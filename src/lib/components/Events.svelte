<script>
	export let events;
</script>

{#if events}
	{#each events as event}
		<span style="font-size: 0.5rem;" class="m-2 bg-warning badge badge-warning text-center">{event.description}</span>
	{/each}
{/if}