<script>
	import { physicals, socials, knowledges, practicals } from './CharacterData.svelte';
	import SecondariesTable from './SecondariesTable.svelte';
	import Specials from './Specials.svelte';
	export let totals;
	export let specials;
</script>

<div class="container">
	<div class="physicals">
		<SecondariesTable labels={physicals} {totals} />
	</div>
	<div class="socials">
		<SecondariesTable labels={socials} {totals} />
	</div>
	<div class="knowledges">
		<SecondariesTable labels={knowledges} {totals} />
	</div>
	<div class="practicals">
		<SecondariesTable labels={practicals} {totals} />
	</div>
	<div class="specials">
		<Specials {specials} />
	</div>
</div>

<style>
	.container {
		display: grid;
		grid-template-columns: repeat(2, max-content);
		gap: 1em;
		grid-template-areas:
			'physicals socials'
			'knowledges practicals'
			'specials specials';
		justify-content: center;
	}
	.physicals {
		grid-area: physicals;
	}
	.socials {
		grid-area: socials;
	}
	.knowledges {
		grid-area: knowledges;
	}
	.practicals {
		grid-area: practicals;
	}
	.specials {
		grid-area: specials;
	}
</style>
