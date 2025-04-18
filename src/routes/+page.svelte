<script>
    import { onMount } from 'svelte';
    import { base } from '$app/paths';
    import { setContext } from 'svelte';
	import DayHeader from '$lib/components/DayHeader.svelte';
	import Day from '$lib/components/Day.svelte';

	let data;
	let tripId = '';
	let trip = null;

	onMount(async () => {
        const response = await fetch(`${base}/data/data.json`);
		if (response.ok) {
            data = await response.json();
			tripId = data.trips[0].id;
		} else {
            console.error('Failed to fetch data:', response.status);
		}
	});
    
	$: trip = data?.trips.find((v) => v.id === tripId);
    setContext('trip', trip)

	function getAccommodation(date){
		let d = new Date(date);
		return trip?.accommodations.find((x) => new Date(x.from) <= d && d < new Date(x.to));
	}
</script>

<div class="container">
	<!-- Sélection du voyage -->
	<div class="row mb-5">
		<select class="form-select" bind:value={tripId}>
			{#each data?.trips ?? [] as v}
				<option value={v.id}>{v.name}</option>
			{/each}
		</select>
	</div>

	<!-- Affichage du voyage -->
	{#if trip}
		{#each trip.days as day, dayIndex}
			<div class="row">
				<div class="accordion" id="accordion{dayIndex}">
					<div class="accordion-item">
						<!-- Date -->
						<h2 class="accordion-header" id="header{dayIndex}">
							<button
								class="accordion-button"
								type="button"
								data-bs-toggle="collapse"
								data-bs-target="#collapse{dayIndex}"
								aria-expanded="true"
								aria-controls="collapse{dayIndex}"
							>                  
                                <DayHeader day={day} />				
							</button>
						</h2>
						<!-- Contenu -->
						<div
							id="collapse{dayIndex}"
							class="accordion-collapse collapse show"
							aria-labelledby="header{dayIndex}"
							data-bs-parent="#accordion{dayIndex}"
						>
							<div class="accordion-body p-0">
								<Day day={day} steps={day.steps} accommodation={getAccommodation(day.date)} countryCurrency={trip.currency} />
							</div>
						</div>
					</div>
				</div>
			</div>
		{/each}
	{/if}
</div>
