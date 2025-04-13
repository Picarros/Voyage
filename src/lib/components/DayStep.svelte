<script>
	import Bullet from '$lib/components/Bullet.svelte';
	import Time from '$lib/components/Time.svelte';
	import Note from '$lib/components/Note.svelte';
	import Address from '$lib/components/Address.svelte';
	import Price from '$lib/components/Price.svelte';

	export let top;
	export let bottom;
	export let step;
	export let countryCurrency;
</script>

<div class="row align-self-center flex-nowrap">
    <div class="col-1 p-0" style="min-width: 30px;">
        <Time time={step.time} utc={step.utc} />
    </div>
    <div class="col-1 p-0" style="min-width: 30px;">
        <Bullet top={top} bottom={bottom} icon={step.type} />
    </div>
    <div class="col-10 p-0 px-2">
        <p class="m-0">
            <span class="fw-bold">
                {step.title}
            </span>
            <span>
                <Price price={step.price} currency={step.currency} {countryCurrency} />
            </span>
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