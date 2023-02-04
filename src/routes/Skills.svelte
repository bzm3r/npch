<script>
	import { physicals, socials, knowledges, practicals } from './CharacterData.svelte';
	import SkillTable from './SkillTable.svelte';
	import Specials from './Specials.svelte';

	export let totals;
	export let specials;

	import { setContext, getContext } from 'svelte';
	import { writable } from 'svelte/store';

	const currentFocus = writable('');

	setContext('currentFocus', currentFocus);

	const currentBreakdown = getContext('currentBreakdown');
	$: $currentBreakdown = $currentFocus != '' ? totals[$currentFocus] : null;
</script>

<div class="container">
	<div class="physicals">
		<SkillTable labels={physicals} {totals} />
	</div>
	<div class="socials">
		<SkillTable labels={socials} {totals} />
	</div>
	<div class="knowledges">
		<SkillTable labels={knowledges} {totals} />
	</div>
	<div class="practicals">
		<SkillTable labels={practicals} {totals} />
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
