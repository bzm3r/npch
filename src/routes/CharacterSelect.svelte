<script>
	import { class_titles, race_titles } from './CharacterData.svelte';
	import SelectBox from './SelectBox.svelte';

	export let race = '';
	export let class1 = '';
	export let class2 = '';
	export let class3 = '';

	let selectBoxDefns = {
		r: {
			name: 'race-select',
			binding: '',
			choices: race_titles,
			humanAcademicSensitive: true
		},
		c1: {
			name: 'c1-select',
			binding: '',
			choices: class_titles,
			humanAcademicSensitive: true
		},
		c2: {
			name: 'c2-select',
			binding: '',
			choices: class_titles,
			humanAcademicSensitive: false
		},
		c3: {
			name: 'c3-select',
			binding: '',
			choices: class_titles,
			humanAcademicSensitive: false
		}
	};
	$: human_academic_style = selectBoxDefns.r.binding === 'Human-Academic' ? 'human_academic' : '';
	$: [race, class1, class2, class3] = Object.values(selectBoxDefns).map((x) => x.binding);
</script>

<div class="selection_boxes">
	{#each Object.keys(selectBoxDefns) as key}
		<SelectBox
			bind:selected={selectBoxDefns[key].binding}
			name={selectBoxDefns[key].name}
			choices={selectBoxDefns[key].choices}
			html_class={selectBoxDefns[key].humanAcademicSensitive ? human_academic_style : ''}
		/>
	{/each}
</div>

<style>
	.selection_boxes {
		display: grid;
		grid-auto-flow: row;
		justify-items: center;
	}
</style>
