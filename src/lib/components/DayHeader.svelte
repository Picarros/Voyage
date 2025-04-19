<script>
	import Calendar from '$lib/components/Calendar.svelte';
	import Events from '$lib/components/Events.svelte';

	export let day;
	export let trip;

	function getEvents(date) {
		let d = new Date(date);
		return trip?.events.filter((x) => new Date(x.from) <= d && d <= new Date(x.to));
	}
</script>

{#if day}
	<div class="container">
		<div class="row justify-content-center">
			<div class="col-auto fw-bold">
				{day.description}
			</div>
		</div>
		<div class="row justify-content-center">
			<div class="col-auto fst-italic">
				<Calendar date={day.date} />
				<Events events={getEvents(day.date)} />
			</div>
		</div>
	</div>
{/if}
