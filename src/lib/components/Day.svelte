<script>
	import Bullet from '$lib/components/Bullet.svelte';
	import Address from '$lib/components/Address.svelte';
	import Price from '$lib/components/Price.svelte';

	export let steps;
	export let accommodation;
	export let countryCurrency;

    console.log(steps.length - 1);
</script>

<div class="container">
	{#if steps}
		{#each steps as step, stepIndex}
			<div class="row align-self-center">
				<div class="col-2">
					<Bullet top={stepIndex != 0} bottom={stepIndex != steps.length - 1 || accommodation != undefined} icon="" />
				</div>
				<div class="col-10">
					<p>
						<span class="fw-bold">{step.title}</span>
					</p>
					<p>Détail</p>
					<hr class="m-0 border border-primary opacity-75" />
				</div>
			</div>
		{/each}
	{/if}
	{#if accommodation}
		<div class="row align-self-center">
			<div class="col-2">
				<Bullet top={true} bottom={false} icon="bed" />
			</div>
			<div class="col-10">
				<p>
					<span class="fw-bold">
						{accommodation.name}
					</span>
					<span>
						(<Price
							price={accommodation.price}
							currency={accommodation.currency}
							{countryCurrency}
						/>)
					</span>
				</p>
				<p>
					<Address address={accommodation.address} />
				</p>
			</div>
		</div>
	{/if}
</div>
