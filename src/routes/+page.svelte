<script>
	import { onMount } from 'svelte';
    import { base } from '$app/paths';

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

    function getDate(date){
        const [day, month, year] = date.split('/');
        return new Date(`${year}-${month}-${day}`);
    }

	$: trip = data?.trips.find((v) => v.id === tripId);
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
						<h2 class="accordion-header" id="header{dayIndex}">
							<button
								class="accordion-button"
								type="button"
								data-bs-toggle="collapse"
								data-bs-target="#collapse{dayIndex}"
								aria-expanded="true"
								aria-controls="collapse{dayIndex}"
							>
								📅 {new Date(getDate(day.date)).toLocaleDateString('fr-FR', {
                                    weekday: 'long',
                                    day: 'numeric',
                                    month: 'long',
                                    year: 'numeric'
                                  })}
							</button>
						</h2>
						<div
							id="collapse{dayIndex}"
							class="accordion-collapse collapse show"
							aria-labelledby="header{dayIndex}"
							data-bs-parent="#accordion{dayIndex}"
						>
							<div class="accordion-body">
								<strong>This is the first item's accordion body.</strong> It is shown by default,
								until the collapse plugin adds the appropriate classes that we use to style each
								element. These classes control the overall appearance, as well as the showing and
								hiding via CSS transitions. You can modify any of this with custom CSS or overriding
								our default variables. It's also worth noting that just about any HTML can go within
								the <code>.accordion-body</code>, though the transition does limit overflow.
							</div>
						</div>
					</div>
				</div>
			</div>
		{/each}
	{/if}
</div>
