<script>
	import { onMount } from 'svelte';
	import { base } from '$app/paths';
	import { setContext } from 'svelte';
	import { trip } from '$lib/components/store.js';
	import DayHeader from '$lib/components/DayHeader.svelte';
	import Day from '$lib/components/Day.svelte';

	let data;
	let tripId = '';
	let allOpen = true;

	onMount(async () => {
		const response = await fetch(`${base}/data/data.json`);
		if (response.ok) {
			data = await response.json();
			tripId = data.trips[0].id;
		} else {
			console.error('Failed to fetch data:', response.status);
		}
	});

	function toggleAll() {
		allOpen = !allOpen;

		if (allOpen) {
			document.querySelectorAll('.accordion-button.collapsed').forEach((ac) => {
				ac.click();
			});
		} else {
			document.querySelectorAll('.accordion-button:not(.collapsed)').forEach((ac) => {
				ac.click();
			});
		}
	}

	$: if (data && tripId) {
		trip.set(data?.trips.find((v) => v.id === tripId));
	}
</script>

<!-- Navbar -->
<nav class="navbar navbar-dark bg-dark sticky-top">
	<div class="container">
		<div class="d-flex w-100">
			<!-- Sélection du voyage -->
			<div class="w-100 pe-2">
				<select class="form-select" bind:value={tripId}>
					{#each data?.trips ?? [] as v}
						<option value={v.id}>{v.name}</option>
					{/each}
				</select>
			</div>
			<!-- Fold / Unfold -->
			<div class="flex-shrink-1">
				<button class="btn btn-primary" on:click={toggleAll}>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						height="20px"
						viewBox="0 -960 960 960"
						width="20px"
						fill="#FFFFFF"
					>
						{#if allOpen}
							<path
								d="m369-192-51-51 162-162 162 162-51 51-111-111-111 111Zm111-363L318-717l51-51 111 111 111-111 51 51-162 162Z"
							/>
						{:else}
							<path
								d="M480-144 318-306l51-51 111 111 111-111 51 51-162 162ZM369-603l-51-51 162-162 162 162-51 51-111-111-111 111Z"
							/>
						{/if}
					</svg>
				</button>
			</div>
		</div>
	</div>
</nav>

<div class="container">
	<!-- Affichage du voyage -->
	{#if $trip}
		{#each $trip.days as day, dayIndex}
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
								<DayHeader {day} />
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
								<Day {day} />
							</div>
						</div>
					</div>
				</div>
			</div>
		{/each}
	{/if}
</div>
