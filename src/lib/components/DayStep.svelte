<script>
	import Bullet from '$lib/components/Bullet.svelte';
	import Time from '$lib/components/Time.svelte';
	import Note from '$lib/components/Note.svelte';
	import Address from '$lib/components/Address.svelte';
	import Price from '$lib/components/Price.svelte';
	import FadeAdapter from '$lib/components/FadeAdapter.svelte';

	export let top;
	export let bottom;
	export let step;

	let days = 0;

	if (step.to && step.from) {
		days = (new Date(step.to) - new Date(step.from)) / (1000 * 60 * 60 * 24);
	}
</script>

<div class="row align-self-center flex-nowrap">
	<div class="col-1 p-0" style="min-width: 45px;">
		<Time time={step.time} utc={step.utc} duration={step.duration} />
	</div>
	<div class="col-1 p-0" style="min-width: 30px;">
		<Bullet {top} {bottom} icon={step.type} />
	</div>
	<div class="col-10 p-0 px-2">
		<p class="m-0">
			<span class="fw-bold">
				{step.description}
			</span>
		</p>
		<p class="position-relative m-0" style="font-size: 0.6rem;">
			<FadeAdapter>
				{#if step.price}
					<div>
						Tot. : <Price price={step.price} currency={step.currency} />
					</div>
				{/if}
				{#if step.price && step.personNumber > 0}
					<div class="position-absolute top-0 start-0">
						1P. : <Price price={step.price / step.personNumber} currency={step.currency} />
					</div>
				{/if}
				{#if step.price && step.personNumber && days > 0}
					<div class="position-absolute top-0 start-0">
						N/P. : <Price price={step.price / step.personNumber / days} currency={step.currency} />
					</div>
				{/if}
			</FadeAdapter>
		</p>
		<p class="m-0">
			<Address address={step.address} />
		</p>
		<p class="m-0">
			<Note note={step.note} danger={step.danger} />
		</p>
		{#if bottom}
			<hr class="m-1 border border-primary opacity-75" />
		{/if}
	</div>
</div>
