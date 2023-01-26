<script>
	export let total_charges;
	export let total_glands;

	// the max number of icons is governed by the number of biotech classes (max classes + 1) = 4
	const max_icons = 4;

	const charge_src = '/charge.svg';
	const gland_src = '/gland.svg';

	const dummy_size = 60;
</script>

<div class="container">
	{#each { length: total_charges } as _}
		<img class="chargeIcon" src={charge_src} alt="charges" title="charges" width="60" height="60" />
	{/each}
	{#each { length: max_icons - total_charges - total_glands } as _}
		<div class="dummy" style:--dummy_size="{dummy_size}px" />
	{/each}
	{#each { length: total_glands } as _}
		<img class="glandIcon" src={gland_src} alt="glands" title="glands" width="60" height="60" />
	{/each}
</div>

<style>
	.container {
		width: 80%;
		display: grid;
		grid-auto-flow: column;
		grid-template-columns: auto;
		margin: 0 auto;
		justify-content: center;
	}

	.dummy {
		width: var(--dummy_size);
	}
</style>
