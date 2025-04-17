<script>
	import { onDestroy } from 'svelte';

	export let time;
	export let utc;
	export let duration;

	let showDeparture = true;
	let interval;

	const hasBoth = time && duration;

	if (hasBoth) {
		interval = setInterval(() => {
			showDeparture = !showDeparture;
		}, 3000);
	}

	onDestroy(() => {
		if (interval) clearInterval(interval);
	});
</script>

<div class="position-relative" style="height: 100%;">
	<div class="position-absolute top-50 start-50 translate-middle text-center">
		
		{#if hasBoth}
			<!-- Bloc Départ -->
			<div class="fade-block" aria-hidden={!showDeparture}>
				{#if time}
					<p class="m-0" style="font-size: 0.8rem;">{time}</p>
				{/if}
				{#if utc}
					<p class="m-0" style="font-size: 0.5rem;">UTC{utc}</p>
				{/if}
			</div>

			<!-- Bloc Durée -->
			<div class="fade-block" aria-hidden={showDeparture}>
				<p class="m-0" style="font-size: 0.8rem;">≈{duration}</p>
			</div>

		{:else if time}
			<!-- Affichage unique : Départ uniquement -->
			<p class="m-0" style="font-size: 0.8rem;">{time}</p>
			{#if utc}
				<p class="m-0" style="font-size: 0.5rem;">UTC{utc}</p>
			{/if}

		{:else if duration}
			<!-- Affichage unique : Durée uniquement -->
			<p class="m-0" style="font-size: 0.8rem;">≈{duration}</p>
		{/if}

	</div>
</div>

<style>
	.fade-block {
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		opacity: 0;
		transition: opacity 0.4s ease;
		pointer-events: none;
	}

	.fade-block[aria-hidden="false"] {
		opacity: 1;
		pointer-events: auto;
	}
</style>
