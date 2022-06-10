<script>
	import { class_titles, race_titles } from './CharacterData.svelte';
  import CharacterSummary from './CharacterSummary.svelte';
	import InputBoxTable from './InputBoxTable.svelte';
	
	let race = "";
	let class1 = "";
	let class2 = "";
	let class3 = "";
</script>

<InputBoxTable bind:race={race} bind:class1={class1} bind:class2={class2} bind:class3={class3}></InputBoxTable>

<CharacterSummary {race} {class1} {class2} {class3}>
</CharacterSummary>
