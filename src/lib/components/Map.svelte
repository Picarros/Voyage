<script>
	export let url;
</script>

{#if url}
	<a class="btn btn-secondary" target="_blank" rel="noopener noreferrer" href={url} role="button">📍</a>
{/if}
