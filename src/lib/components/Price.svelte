<script>
	import { onMount } from 'svelte';

	export let price;
	export let currency; // Devise d'entrée (ex: 'USD')
	export let countryCurrency; // Devise cible (ex: 'EUR')

	let rates = {};
	let priceEUR = '';
	let priceCUR = '';

	// Récupération des taux à partir de la devise de référence (ici EUR)
	async function fetchRates() {
		const res = await fetch('https://open.er-api.com/v6/latest/EUR');
		const data = await res.json();

		if (data.result === 'success') {
			rates = data.rates;
			updatePrices();
		} else {
			console.error('Erreur de récupération des taux');
		}
	}

	function updatePrices() {
		if (!price || !currency || !countryCurrency || !rates[countryCurrency]) return;

		// Si la devise entrée est EUR
		if (currency === 'EUR') {
			priceEUR = formatCurrency(price, 'EUR');
			priceCUR = formatCurrency(price * rates[countryCurrency], countryCurrency);
		}
		// Si la devise entrée est autre
		else {
			const eurPrice = price / rates[currency]; // Conversion en EUR
			priceEUR = formatCurrency(eurPrice, 'EUR');
			priceCUR = formatCurrency(price, currency);
		}
	}

	function formatCurrency(value, currencyCode) {
		return new Intl.NumberFormat('fr-FR', {
			style: 'currency',
			currency: currencyCode
		}).format(value);
	}

	// Met à jour les prix si l'une des entrées change
	$: if (price && rates && currency && countryCurrency) {
		updatePrices();
	}

	onMount(fetchRates);
</script>

{#if priceEUR && priceCUR}
	<span style="font-size: 0.8rem;" class="fst-italic">
		(
		<span class={currency == 'EUR' ? 'text-decoration-underline' : ''}>
			{priceEUR}
		</span>
		{#if countryCurrency != 'EUR'}
			<span> / </span>
			<span class={currency != 'EUR' ? 'text-decoration-underline' : ''}>
				{priceCUR}
			</span>
		{/if}
		)
	</span>
{/if}
