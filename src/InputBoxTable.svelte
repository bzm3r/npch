<script>
	import { class_titles, race_titles } from './CharacterData.svelte';
	import InputBoxRow from './InputBoxRow.svelte';
	
	export let race = "";
	export let class1 = "";
	export let class2 = "";
	export let class3 = "";
	
	$: selectable_races = race_titles.filter(race_title => race_title != race);
	$: selectable_classes = class_titles.filter(class_title => class_title != class1 && class_title != class2 && class_title != class3);
</script>

<table>
	<InputBoxRow bind:selected={race} title="Race" name="race-select" choices={selectable_races}></InputBoxRow>
	<InputBoxRow bind:selected={class1} title="Class 1" name="c1-select" choices={selectable_classes}></InputBoxRow>
	<InputBoxRow bind:selected={class2} title="Class 2" name="c2-select" choices={selectable_classes}></InputBoxRow>
	<InputBoxRow bind:selected={class3} title="Class 3" name="c3-select" choices={selectable_classes}></InputBoxRow>
</table>
