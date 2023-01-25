<script>
	export let total_charges;
	export let total_glands;

	const charge_src = '/charge.svg';
	const gland_src = '/gland.svg';
</script>

<div class="wrapper">
	{#if total_charges + total_glands > 0}
		<div class="charge_container">
			{#each { length: total_charges } as _}
				<img class="chargeIcon" src={charge_src} alt="charges" title="charges" height="60" />
			{/each}
		</div>
	{/if}

	{#if total_glands > 0}
		<div class="gland_container">
			{#each { length: total_glands } as _}
				<img class="glandIcon" src={gland_src} alt="glands" title="glands" height="60" />
			{/each}
		</div>
	{/if}
</div>

<style>
	.wrapper {
		display: grid;
		grid-template-columns: repeat(2, 125px);
		grid-template-rows: 1fr;
		grid-template-areas: 'charge_container' 'gland_container';
		column-gap: 20px;
	}

	.charge_container {
		grid-area: 'charge_container';
		display: grid;
		grid-auto-flow: column;
		grid-template-columns: auto;
		grid-template-rows: 1fr;
		column-gap: 20px;
		justify-content: start;
	}

	.gland_container {
		grid-area: 'gland_container';
		display: grid;
		grid-auto-flow: column;
		grid-template-columns: auto;
		grid-template-rows: 1fr;
		column-gap: 20px;
		justify-content: end;
	}
</style>
