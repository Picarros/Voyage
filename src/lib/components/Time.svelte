<script>
	export let time;
	export let utc;

	function Compare(s1, s2) {
		return s1.toUpperCase() === s2.toUpperCase();
	}
</script>

<div class="position-relative" style="height: 100%">
{#if time && utc}
	<div class="position-absolute top-50 start-50 translate-middle">
        <p style="font-size: 0.8rem;" class="m-0 text-center">{time}</p>
        <p style="font-size: 0.5rem;" class="m-0 text-center">UTC{utc}</p>
    </div>
{/if}
</div>
