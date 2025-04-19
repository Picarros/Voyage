<script>
	import DayStep from '$lib/components/DayStep.svelte';

	export let day;
	export let trip;

	function getAccommodation(date) {
		let d = new Date(date);
		return trip?.accommodations.find((x) => new Date(x.from) <= d && d < new Date(x.to));
	}

	$: accommodation = getAccommodation(day.date);
</script>

<div class="container">
	{#if day.steps}
		{#each day.steps as step, stepIndex}
			<DayStep
				top={stepIndex != 0}
				bottom={stepIndex != day.steps.length - 1 || accommodation != undefined}
				step={step}
				countryCurrency={trip?.currency}
			/>
		{/each}
	{/if}
	{#if accommodation}
		<DayStep
			top={true}
			bottom={false}
			step={accommodation}
			countryCurrency={trip?.currency}
		/>
	{/if}
</div>
