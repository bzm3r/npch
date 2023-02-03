<script>
	import { classTitles, raceTitles, races, classes } from './CharacterData.svelte';
	import SelectBox from './SelectBox.svelte';

	export let race = '';
	export let class1 = '';
	export let class2 = '';
	export let class3 = '';

	class CompatibilityError {
		constructor() {
			this.biotechIssue = false;
			this.duplicateIssue = false;
		}
		reset() {
			this.biotechIssue = false;
			this.duplicateIssue = false;
		}
		any() {
			return this.biotechIssue || this.duplicateIssue;
		}
	}

	let selectBoxDefns = {
		r: {
			name: 'race-select',
			value: '',
			error: new CompatibilityError(),
			choices: raceTitles,
			humanAcademicSensitive: true
		},
		c1: {
			name: 'c1-select',
			value: '',
			error: new CompatibilityError(),
			choices: classTitles,
			humanAcademicSensitive: true
		},
		c2: {
			name: 'c2-select',
			value: '',
			error: new CompatibilityError(),
			choices: classTitles,
			humanAcademicSensitive: false
		},
		c3: {
			name: 'c3-select',
			value: '',
			error: new CompatibilityError(),
			choices: classTitles,
			humanAcademicSensitive: false
		}
	};

	function isInvalid(selection) {
		return selection === '' || selection === undefined;
	}

	function checkCompatibility(selectBoxDefns) {
		Object.values(selectBoxDefns).forEach((x) => x.error.reset());

		if (!isInvalid(selectBoxDefns.r.value)) {
			if (races.get(selectBoxDefns.r.value)['Robotic'] === 1) {
				if (
					!isInvalid(selectBoxDefns.c1.value) &&
					classes.get(selectBoxDefns.c1.value)['Glands'] > 0
				) {
					selectBoxDefns.c1.error.biotechIssue = true;
				}
				if (
					!isInvalid(selectBoxDefns.c2.value) &&
					classes.get(selectBoxDefns.c2.value)['Glands'] > 0
				) {
					selectBoxDefns.c2.error.biotechIssue = true;
				}
				if (
					!isInvalid(selectBoxDefns.c3.value) &&
					classes.get(selectBoxDefns.c3.value)['Glands'] > 0
				) {
					selectBoxDefns.c3.error.biotechIssue = true;
				}
				if (
					selectBoxDefns.c1.error.biotechIssue ||
					selectBoxDefns.c2.error.biotechIssue ||
					selectBoxDefns.c3.error.biotechIssue
				) {
					selectBoxDefns.r.error.biotechIssue = true;
				}
			}
		}
		if (
			selectBoxDefns.c1.value != '' &&
			selectBoxDefns.c2.value != '' &&
			selectBoxDefns.c1.value === selectBoxDefns.c2.value
		) {
			selectBoxDefns.c1.error.duplicateIssue = true;
			selectBoxDefns.c2.error.duplicateIssue = true;
		}
		if (
			selectBoxDefns.c2.value != '' &&
			selectBoxDefns.c3.value != '' &&
			selectBoxDefns.c2.value === selectBoxDefns.c3.value
		) {
			selectBoxDefns.c2.error.duplicateIssue = true;
			selectBoxDefns.c3.error.duplicateIssue = true;
		}
		if (
			selectBoxDefns.c1.value != '' &&
			selectBoxDefns.c3.value != '' &&
			selectBoxDefns.c1.value === selectBoxDefns.c3.value
		) {
			selectBoxDefns.c1.error.duplicateIssue = true;
			selectBoxDefns.c3.error.duplicateIssue = true;
		}
	}

	$: checkCompatibility(selectBoxDefns);

	$: human_academic_style = selectBoxDefns.r.value === 'Human-Academic' ? 'human_academic' : '';
	$: [race, class1, class2, class3] = Object.values(selectBoxDefns).map((x) => x.value);

	import { getContext } from 'svelte';
	const currentBreakdown = getContext('currentBreakdown');
	$: breakdownText = $currentBreakdown
		? $currentBreakdown.partials
				.map((partial) => {
					console.log(partial.sources.join(' * '));
					return partial.sources.join(' * ') + ': ' + partial.value;
					// partial.sources.map((sources) => sources.join(' + ')).join(' * ') + ': ' + partial.value;
				})
				.join('; ')
		: 'empty';
</script>

<div class="selection_boxes">
	{#each Object.keys(selectBoxDefns) as key}
		<div class="dummy" />
		<div class="select-box">
			<SelectBox
				bind:selected={selectBoxDefns[key].value}
				name={selectBoxDefns[key].name}
				choices={selectBoxDefns[key].choices}
				html_class={selectBoxDefns[key].humanAcademicSensitive ? human_academic_style : ''}
			/>
		</div>
		<div class="issue-icons">
			<div class="biotech-issue">
				{#if selectBoxDefns[key].error.biotechIssue}
					<img
						class="biotech-issue-icon"
						src="/biotech-issue.svg"
						alt="robotic races are incompatible with biotech"
						title="robotic races are incompatible with biotech"
					/>
				{/if}
			</div>
			<div class="duplicate-issue">
				{#if selectBoxDefns[key].error.duplicateIssue}
					<img
						class="duplicate-issue-icon"
						src="/duplicate-issue.svg"
						alt="duplicate of another class"
						title="duplicate of another class"
					/>
				{/if}
			</div>
		</div>
	{/each}
</div>
<div>breakdown: {breakdownText}</div>

<!-- {#if Object.values(selectBoxDefns).some((x) => x.error.biotechIssue || x.error.duplicateIssue)}
	<div class="dummy" />
	<div class="warnings">
		<b>Warnings: </b>
		<ul>
			{#if Object.values(selectBoxDefns).some((x) => x.error.biotechIssue)}
				<li>
					<img
						class="biotech-issue-icon"
						src="/biotech-issue.svg"
						alt="robotic races are incompatible with biotech"
						title="robotic races are incompatible with biotech"
					/> Robotic races are incompatible with biotech classes
				</li>
			{/if}
			{#if Object.values(selectBoxDefns).some((x) => x.error.duplicateIssue)}
				<li>
					<img
						class="duplicate-issue-icon"
						src="/duplicate-issue.svg"
						alt="duplicate of another class"
						title="duplicate of another class"
					/> Duplicate of another class
				</li>
			{/if}
		</ul>
	</div>
	<div class="dummy" />
{/if} -->
<style>
	.selection_boxes {
		display: grid;
		grid-auto-flow: row;
		grid-template-columns: 5rem 11rem 5rem;
		grid-template-areas: repeat(4, 'dummy select-box issue-icons');
		justify-self: center;
		justify-content: center;
		column-gap: 0.5em;
	}

	.biotech-issue-icon {
		width: 2rem;
		justify-self: center;
		justify-content: center;
	}
	.duplicate-issue-icon {
		width: 2rem;
	}
	.issue-icons {
		display: grid;
		grid-auto-flow: row;
		grid-template-columns: repeat(2, max-content);
	}
	.dummy {
		grid-area: 'dummy';
	}
	.select-box {
		grid-area: 'select-box';
	}
	.issue-icons {
		grid-area: 'issue-icons';
	}
</style>
