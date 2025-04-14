<script>
	export let note;
    export let danger;
</script>

{#if note}
<div class="d-flex align-items-center gap-2">
    <span class="badge bg-secondary">Note</span>
    <span style="font-size: 0.8rem;" class="text-secondary">{@html note}</span>
</div>
{/if}
{#if danger}
<div class="d-flex align-items-center gap-2">
    <span class="badge bg-danger">Attention</span>
    <span style="font-size: 0.8rem;" class="text-danger">{@html danger}</span>
</div>
{/if}