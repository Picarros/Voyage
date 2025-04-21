<script>
	import { onDestroy } from 'svelte';
	import FadeAdapter from '$lib/components/FadeAdapter.svelte';

	export let time;
	export let utc;
	export let duration;
</script>

<div class="position-relative" style="height: 100%;">
	<FadeAdapter>
		{#if time || utc}
			<div class="position-absolute top-50 start-50 translate-middle">
				{#if time}
					<p class="m-0 text-center" style="font-size: 0.8rem;">{time}</p>
				{/if}
				{#if utc}
					<p class="m-0 text-center" style="font-size: 0.5rem;">UTC{utc}</p>
				{/if}
			</div>
		{/if}
		{#if duration}
			<div class="position-absolute top-50 start-50 translate-middle">
				<p class="m-0 text-center" style="font-size: 0.8rem;">≈{duration}</p>
			</div>
		{/if}
	</FadeAdapter>
</div>
