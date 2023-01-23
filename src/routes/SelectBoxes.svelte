<script>
	import { class_titles, race_titles } from './CharacterData.svelte';
	import SelectBox from './SelectBox.svelte';

	export let race = '';
	export let class1 = '';
	export let class2 = '';
	export let class3 = '';

	$: selectable_races = race_titles.filter((race_title) => race_title != race);
	$: selectable_classes = class_titles.filter(
		(class_title) => class_title != class1 && class_title != class2 && class_title != class3
	);
	$: human_academic_style = race === 'Human-Academic' ? 'human_academic' : '';
</script>

<div class="container">
	<SelectBox
		bind:selected={race}
		name="race-select"
		choices={selectable_races}
		html_class={human_academic_style}
	/>
	<SelectBox
		bind:selected={class1}
		name="c1-select"
		choices={selectable_classes}
		html_class={human_academic_style}
	/>
	<SelectBox bind:selected={class2} name="c2-select" choices={selectable_classes} />
	<SelectBox bind:selected={class3} name="c3-select" choices={selectable_classes} />
</div>

<style>
	.container {
		display: grid;
		grid-template-rows: repeat(4, 1fr);
		justify-content: center;
	}
</style>
