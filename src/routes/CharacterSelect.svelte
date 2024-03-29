<script>
	import { classTitles, raceTitles, races, classes } from './CharacterData.svelte';
	import SelectBox from './SelectBox.svelte';
	import BreakDownInfo from './BreakDownInfo.svelte';

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

	$: selectBoxDefns = {
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

	import { getContext } from 'svelte';
	const currentBreakdown = getContext('currentBreakdown');

	$: human_academic_style = selectBoxDefns.r.value === 'Human-Academic' ? 'human_academic' : '';
	$: [race, class1, class2, class3] = Object.values(selectBoxDefns).map((x) => x.value);
</script>

<div class="selection_boxes">
	{#each Object.keys(selectBoxDefns) as key}
		<div class="issue-area">
			{#if selectBoxDefns[key].error.biotechIssue}
				<div class="biotech-issue">
					<img
						class="biotech-issue-icon"
						src="/biotech-issue.svg"
						alt="robotic races are incompatible with biotech"
						title="robotic races are incompatible with biotech"
					/>
				</div>
			{/if}
			{#if selectBoxDefns[key].error.duplicateIssue}
				<div class="duplicate-issue">
					<img
						class="duplicate-issue-icon"
						src="/duplicate-issue.svg"
						alt="duplicate of another class"
						title="duplicate of another class"
					/>
				</div>
			{/if}
		</div>
		<div class="select-box">
			<SelectBox
				bind:selected={selectBoxDefns[key].value}
				name={selectBoxDefns[key].name}
				choices={selectBoxDefns[key].choices}
				html_class={selectBoxDefns[key].humanAcademicSensitive ? human_academic_style : ''}
			/>
		</div>
		<div class="info-area">
			{#if $currentBreakdown && Array.from($currentBreakdown.partials.keys()).includes(selectBoxDefns[key].value)}
				<div class="breakdown-info">
					<BreakDownInfo
						id={$currentBreakdown.id}
						value={$currentBreakdown.id === 'special'
							? ''
							: $currentBreakdown.partials.get(selectBoxDefns[key].value)}
					/>
				</div>
			{/if}
		</div>
	{/each}
</div>

<style>
	.selection_boxes {
		display: grid;
		grid-auto-flow: row;
		grid-template-columns: 8rem 11rem 8rem;
		grid-template-areas: repeat(4, 'issue-area select-box info-area');
		justify-self: center;
		justify-content: center;
		column-gap: 0.5em;
	}

	.biotech-issue-icon {
		height: 2.5rem;
		width: 2rem;
	}

	.duplicate-issue-icon {
		height: 2.5rem;
		width: 2rem;
	}

	.issue-area {
		height: 2.5rem;
		width: 4rem;
		display: flex;
		align-items: center;
		justify-content: flex-end;
		justify-self: end;
		gap: 0.2rem;
		grid-area: 'issue-area';
	}

	.select-box {
		grid-area: 'select-box';
	}

	.info-area {
		height: 2.5rem;
		width: 4rem;
		display: flex;
		align-items: center;
		justify-content: flex-start;
		gap: 0.2rem;
		grid-area: 'info-area';
	}
</style>
