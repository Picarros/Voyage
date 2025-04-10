<script>
	import Map from '$lib/components/Map.svelte';
	import Price from '$lib/components/Price.svelte';

	export let steps;
	export let accommodation;
	export let countryCurrency;
</script>

<div class="container">
	{#if steps}
		<div class="row align-self-center">
			<p>TOTO</p>
		</div>
	{/if}
	{#if accommodation}
		<div class="row align-self-center">
            <div class="col-2">
                <div class="position-relative" style="height: 100%">
                    <!-- Barre du haut -->
                    <div class="position-absolute top-0 start-50 translate-middle-x"
                        style="
                            width: 4px;
                            height: 50%;
                            background-color: green;">
                    </div>
                    <!-- Barre du bas -->
                    <div class="position-absolute bottom-0 start-50 translate-middle-x"
                    style="
                        width: 4px;
                        height: 50%;
                        background-color: green;">
                    </div>
                    <!-- Cercle -->
                    <div class="position-absolute top-50 start-50 translate-middle"
                        style="
                            width: 25px;
                            height: 25px;
                            background-color: green;
                            border-radius: 50%;">
                    </div>
                    <!-- Icone -->
                    <!-- Lit -->
                    <svg xmlns="http://www.w3.org/2000/svg" class="position-absolute top-50 start-50 translate-middle" height="20px" viewBox="0 -960 960 960" width="20px" fill="#FFFFFF"><path d="M80-200v-240q0-27 11-49t29-39v-112q0-50 35-85t85-35h160q23 0 43 8.5t37 23.5q17-15 37-23.5t43-8.5h160q50 0 85 35t35 85v112q18 17 29 39t11 49v240h-80v-80H160v80H80Zm440-360h240v-80q0-17-11.5-28.5T720-680H560q-17 0-28.5 11.5T520-640v80Zm-320 0h240v-80q0-17-11.5-28.5T400-680H240q-17 0-28.5 11.5T200-640v80Zm-40 200h640v-80q0-17-11.5-28.5T760-480H200q-17 0-28.5 11.5T160-440v80Zm640 0H160h640Z"/></svg>
                </div>
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
                    <a
                        class="fst-italic"
                        target="_blank"
                        rel="noopener noreferrer"
                        href="https://www.google.com/maps/place/{accommodation.address}"
                    >
                        {accommodation.address}
                    </a>
                    <span>
                        <!-- <Map url={accommodation.map} /> -->
                    </span>
                </p>
            </div>
		</div>
	{/if}
</div>
