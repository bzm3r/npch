<script>
	import CharacterSummary from './CharacterSummary.svelte';
	import SelectBoxes from './SelectBoxes.svelte';
	
	let race = "";
	let class1 = "";
	let class2 = "";
	let class3 = "";
</script>

<SelectBoxes bind:race={race} bind:class1={class1} bind:class2={class2} bind:class3={class3}></SelectBoxes>

<CharacterSummary {race} {class1} {class2} {class3}>
</CharacterSummary>

