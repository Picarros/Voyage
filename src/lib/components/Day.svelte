<script>
	import Bullet from '$lib/components/Bullet.svelte';
	import Time from '$lib/components/Time.svelte';
	import Note from '$lib/components/Note.svelte';
	import Address from '$lib/components/Address.svelte';
	import Price from '$lib/components/Price.svelte';
	import DayStep from './DayStep.svelte';

	export let steps;
	export let accommodation;
	export let countryCurrency;
</script>

<div class="container">
	{#if steps}
		{#each steps as step, stepIndex}
			<DayStep
				top={stepIndex != 0}
				bottom={stepIndex != steps.length - 1 || accommodation != undefined}
				step={step}
				countryCurrency={countryCurrency}
			/>
		{/each}
	{/if}
	{#if accommodation}
		<DayStep top={true} 
                bottom={false} 
                step={accommodation} 
                countryCurrency={countryCurrency} />
	{/if}
</div>
