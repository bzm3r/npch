<script>
    import { primaries1, primaries2 } from './CharacterData.svelte';
	import Specials from './Specials.svelte';
	import PrimariesRow from './PrimariesRow.svelte';

    export let totals;
	export let specials;
</script>

<div class="container">
	<div class="primaries1">
		<PrimariesRow primaries={primaries1} {totals}></PrimariesRow>
	</div>
	<div class="primaries2">
		<PrimariesRow primaries={primaries2} {totals}></PrimariesRow>
	</div>
	<div class="specials">
		<Specials {specials}></Specials>
	</div>
</div>

<style>
    .container {
        display: grid;
        grid-template-columns: auto;
        grid-template-rows: auto;
        grid-template-areas:
        "primaries1"
        "primaries2"
        "specials";
    }
    .primaries1 {
        justify-self: center;
        grid-area: primaries1;
    }
    .primaries2 {
        justify-self: center;
        grid-area: primaries2;
    }
    .specials {
        justify-self: center;
        grid-area: specials;
    }
</style>
