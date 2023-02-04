<script>
	export let total_charges;
	export let total_glands;

	// the max number of icons is governed by the number of biotech classes (max classes + 1) = 4
	const max_icons = 4;

	const charge_src = '/charge.svg';
	const gland_src = '/gland.svg';

	const dummy_size = 60;

	import { getContext } from 'svelte';
	const currentFocus = getContext('currentFocus');

	function handleClick(id) {
		if ($currentFocus === id) {
			$currentFocus = '';
		} else {
			$currentFocus = id;
		}
	}
</script>

<div class="container">
	{#each { length: total_charges } as _}
		<img
			class={'charge-icon'}
			src={charge_src}
			alt="charges"
			title="charges"
			width="60"
			height="60"
			on:click={() => handleClick('Charges')}
			on:keydown={() => handleClick('Charges')}
			style={$currentFocus === 'Charges' ? 'background-color: gold;' : ''}
		/>
	{/each}
	{#each { length: max_icons - total_charges - total_glands } as _}
		<div class="dummy" style:--dummy_size="{dummy_size}px" />
	{/each}
	{#each { length: total_glands } as _}
		<img
			class={'gland-icon'}
			src={gland_src}
			alt="glands"
			title="glands"
			width="60"
			height="60"
			on:click={() => handleClick('Glands')}
			on:keydown={() => handleClick('Glands')}
			style={$currentFocus === 'Glands' ? 'background-color: gold;' : ''}
		/>
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
