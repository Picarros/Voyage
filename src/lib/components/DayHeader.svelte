<script>
	import Calendar from '$lib/components/Calendar.svelte';
	import Events from '$lib/components/Events.svelte';
	import { trip } from '$lib/components/store.js';

	export let day;

	function getEvents(date) {
		let d = new Date(date);
		return $trip?.events.filter((x) => new Date(x.from) <= d && d <= new Date(x.to));
	}
    $: events = getEvents(day.date);
</script>

{#if day}
	<div class="container">
		<div class="row justify-content-center">
			<div class="col-auto fw-bold text-center">
				{day.description}
			</div>
		</div>
		<div class="row justify-content-center">
			<div class="col-auto fst-italic text-center">
				<Calendar date={day.date} />
				<Events events={events} />
			</div>
		</div>
	</div>
{/if}
