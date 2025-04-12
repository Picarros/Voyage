<script>
	export let top;
	export let bottom;
	export let icon;
</script>

<div class="position-relative" style="height: 100%">
	<!-- Barre du haut -->
	{#if top == true}
		<div
			class="position-absolute top-0 start-50 translate-middle-x"
			style="
            width: 4px;
            height: 50%;
            background-color: green;"
		></div>
	{/if}
	{#if bottom == true}
		<!-- Barre du bas -->
		<div
			class="position-absolute bottom-0 start-50 translate-middle-x"
			style="
        width: 4px;
        height: 50%;
        background-color: green;"
		></div>
	{/if}
	<!-- Cercle -->
	<div
		class="position-absolute top-50 start-50 translate-middle"
		style="
            width: 25px;
            height: 25px;
            background-color: green;
            border-radius: 50%;"
	></div>
	<!-- Icones -->
	<svg
		xmlns="http://www.w3.org/2000/svg"
		class="position-absolute top-50 start-50 translate-middle"
		height="20px"
		viewBox="0 -960 960 960"
		width="20px"
		fill="#FFFFFF"
	>
		<!-- Lit -->
		{#if icon == 'bed'}
			<path
				d="M80-200v-240q0-27 11-49t29-39v-112q0-50 35-85t85-35h160q23 0 43 8.5t37 23.5q17-15 37-23.5t43-8.5h160q50 0 85 35t35 85v112q18 17 29 39t11 49v240h-80v-80H160v80H80Zm440-360h240v-80q0-17-11.5-28.5T720-680H560q-17 0-28.5 11.5T520-640v80Zm-320 0h240v-80q0-17-11.5-28.5T400-680H240q-17 0-28.5 11.5T200-640v80Zm-40 200h640v-80q0-17-11.5-28.5T760-480H200q-17 0-28.5 11.5T160-440v80Zm640 0H160h640Z"
			/>
        <!-- Défaut -->
		{:else}
			<path
				d="M552-96v-213l-76-75-32 160-252-51 14-70 181 36 52-263-79 34v106h-72v-154l185-78q9-4 18.5-6t19.5-2q27 0 48.5 12.5T595-623l14 23q30 51 68 73.5t91 22.5v72q-57 0-106.5-25T577-528l-23 120 70 70v242h-72Zm24-600q-35 0-59.5-24.5T492-780q0-35 24.5-59.5T576-864q35 0 59.5 24.5T660-780q0 35-24.5 59.5T576-696Z"
			/>
		{/if}
	</svg>
</div>
