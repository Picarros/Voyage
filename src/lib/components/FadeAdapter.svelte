<script>   
    let displayDuration = 2000;
	let transitionDuration = 500;
    
	import { onMount } from 'svelte';
	let { children } = $props();
    
	let visible = true;
	let index = 0;
	let slottedChildren;
    
    let container;

	onMount(async () => {
		// Accède aux enfants passés dans le slot
		slottedChildren = Array.from(container.children);

        // On vérifie qu'il y a plus qu'un élément
		if (slottedChildren.length > 1) {

			// Cache tous sauf le premier
			slottedChildren.forEach((el, i) => {
				el.style.transition = `opacity ${transitionDuration}ms ease-in-out`;
				el.style.opacity = i === 0 ? 1 : 0;
			});

			const loop = () => {
				// fade out current
				if (slottedChildren[index] != undefined) {
					slottedChildren[index].style.opacity = 0;
				}

				setTimeout(() => {
					index = (index + 1) % slottedChildren.length;
					// fade in next
					if (slottedChildren[index] != undefined) {
						slottedChildren[index].style.opacity = 1;
					}

					setTimeout(loop, displayDuration);
				}, transitionDuration);
			};

			setTimeout(loop, displayDuration);
		}
	});
</script>

<span bind:this={container}>
    {@render children?.()}
</span>