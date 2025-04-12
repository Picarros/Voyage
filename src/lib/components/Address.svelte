<script>
	export let address;
	const adresseEncodee = encodeURIComponent(address);
	const url = `https://www.google.com/maps?q=${adresseEncodee}`;
</script>

{#if url}
	<a class="fst-italic" target="_blank" rel="noopener noreferrer" href={url}>
		{address}
	</a>
{/if}