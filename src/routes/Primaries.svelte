<script>
	import { primaries1, primaries2 } from './CharacterData.svelte';
	import PrimariesRow from './PrimariesRow.svelte';
	import ChargesAndGlands from './ChargesAndGlands.svelte';
	import Specials from './Specials.svelte';

	export let totals;
	export let specials;

	$: total_charges = totals['Charges'].total > 0 ? totals['Charges'].total : 0;
	$: total_glands = totals['Glands'].total > 0 ? totals['Glands'].total + 1 : 0;
</script>

<div class="container">
	<div class="primaries1">
		<PrimariesRow primaries={primaries1} {totals} />
	</div>
	<div class="primaries2">
		<PrimariesRow primaries={primaries2} {totals} />
	</div>
	<div class="charges_and_glands">
		<ChargesAndGlands {total_charges} {total_glands} />
	</div>
	<div class="specials">
		<Specials {specials} />
	</div>
</div>

<style>
	.container {
		display: grid;
		grid-auto-flow: row;
		grid-template-areas: 'primaries1' 'primaries2' 'charges_and_glands' 'specials';
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
	.specials {
		grid-area: specials;
	}
</style>
