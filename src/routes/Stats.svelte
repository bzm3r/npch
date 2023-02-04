<script>
	import { primaries1, primaries2 } from './CharacterData.svelte';
	import StatsRow from './StatsRow.svelte';
	import ChargesAndGlands from './ChargesAndGlands.svelte';
	import Specials from './Specials.svelte';

	export let totals;
	export let specials;

	import { setContext, getContext } from 'svelte';
	import { writable } from 'svelte/store';

	const currentFocus = writable('');

	setContext('currentFocus', currentFocus);

	const currentBreakdown = getContext('currentBreakdown');

	function fetchBreakdown(id) {
		if (id) {
			let breakdown = totals[id];
			if (!breakdown) {
				return specials.find((special) => special.special_id === id);
			} else {
				return breakdown;
			}
		} else {
			return null;
		}
	}
	$: totals, specials, ($currentBreakdown = fetchBreakdown($currentFocus));

	$: total_charges = totals['Charges'].value > 0 ? totals['Charges'].value : 0;
	$: total_glands = totals['Glands'].value > 0 ? totals['Glands'].value + 1 : 0;
</script>

<div class="container">
	<div class="primaries1">
		<StatsRow primaries={primaries1} {totals} />
	</div>
	<div class="primaries2">
		<StatsRow primaries={primaries2} {totals} />
	</div>
	<div class="charges_and_glands">
		<ChargesAndGlands {total_charges} {total_glands} />
	</div>
</div>

<div class="specials">
	<Specials {specials} />
</div>

<style>
	.container {
		display: grid;
		grid-auto-flow: row;
		grid-template-areas: 'primaries1' 'primaries2' 'charges_and_glands';
	}
	.primaries1 {
		grid-area: primaries1;
	}
	.primaries2 {
		grid-area: primaries2;
	}
	.charges_and_glands {
		grid-area: charges_and_glands;
	}
</style>
