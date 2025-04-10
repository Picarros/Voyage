<script>
	export let date;
</script>

{#if date}
	📅 {new Date(date).toLocaleDateString('fr-FR', {
		weekday: 'long',
		day: 'numeric',
		month: 'long',
		year: 'numeric'
	})}
{/if}
