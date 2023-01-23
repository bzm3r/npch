<script>
	import { all_labels, races, classes } from './CharacterData.svelte';
	import Primaries from './Primaries.svelte';
	import Secondaries from './Secondaries.svelte';
	import Specials from './Specials.svelte';
	import Tabs from './Tabs.svelte';
	import Tab from './Tab.svelte';

	export let race = '';
	export let class1 = '';
	export let class2 = '';
	export let class3 = '';

	let r_dat = null;
	let c1_dat = null;
	let c2_dat = null;
	let c3_dat = null;

	let titles = [];
	let totals = new Map();
	let primary_specials = [];
	let skill_specials = [];
	let flavor_specials = [];
	let equipment = [];

	function updateTitles(r_dat, c1_dat, c2_dat, c3_dat) {
		titles = [];
		[r_dat, c1_dat, c2_dat, c3_dat].forEach((dat) => {
			if (dat != null) {
				titles.push(dat.title);
			}
		});
	}

	function updateSpecials(r_dat, c1_dat, c2_dat, c3_dat) {
		primary_specials = [];
		skill_specials = [];
		flavor_specials = [];
		equipment = [];
		[r_dat, c1_dat, c2_dat, c3_dat].forEach((dat) => {
			if (dat != null) {
				primary_specials.push(...dat.specials.primary);
				skill_specials.push(...dat.specials.skill);
				flavor_specials.push(...dat.specials.flavor);
				equipment.push(...dat.specials.equipment);
			}
		});

		if (r_dat != null && r_dat.title === 'Human-Academic') {
			if (c1_dat != null) {
				primary_specials.push(...c1_dat.specials.primary);
				primary_specials.push(...c1_dat.specials.skill);
			}
		}
	}

	function updateTotals(r_dat, c1_dat, c2_dat, c3_dat) {
		for (const label of all_labels) {
			totals[label] = 0;
			if (r_dat != null) {
				totals[label] += r_dat[label];
			}
			if (c1_dat != null) {
				if (r_dat != null && r_dat.title === 'Human-Academic') {
					totals[label] += 2 * c1_dat[label];
				} else {
					totals[label] += c1_dat[label];
				}
			}
			if (c2_dat != null) {
				totals[label] += c2_dat[label];
			}
			if (c3_dat != null) {
				totals[label] += c3_dat[label];
			}
		}
	}

	let tabs = [
		{
			id: 0,
			title: 'Primaries',
			component: Primaries,
			inputs: { totals: totals, specials: primary_specials }
		},
		{
			id: 1,
			title: 'Secondaries',
			component: Secondaries,
			inputs: { totals: totals, specials: skill_specials }
		},
		{
			id: 2,
			title: 'Specials',
			component: Specials,
			inputs: { specials: flavor_specials }
		},
		{
			id: 3,
			title: 'Equipment',
			component: Specials,
			inputs: { specials: equipment }
		}
	];

	$: if (race != '') {
		r_dat = races.get(race);
	} else {
		r_dat = null;
	}
	$: if (class1 != '') {
		c1_dat = classes.get(class1);
	} else {
		c1_dat = null;
	}
	$: if (class2 != '') {
		c2_dat = classes.get(class2);
	} else {
		c2_dat = null;
	}
	$: if (class3 != '') {
		c3_dat = classes.get(class3);
	} else {
		c2_dat = null;
	}

	$: updateTitles(r_dat, c1_dat, c2_dat, c3_dat);
	$: updateSpecials(r_dat, c1_dat, c2_dat, c3_dat);
	$: updateTotals(r_dat, c1_dat, c2_dat, c3_dat);
	$: tabs = [
		{
			id: 0,
			title: 'Primaries',
			component: Primaries,
			inputs: { totals: totals, specials: primary_specials }
		},
		{
			id: 1,
			title: 'Secondaries',
			component: Secondaries,
			inputs: { totals: totals, specials: skill_specials }
		},
		{
			id: 2,
			title: 'Specials',
			component: Specials,
			inputs: { specials: flavor_specials }
		},
		{
			id: 3,
			title: 'Equipment',
			component: Specials,
			inputs: { specials: equipment }
		}
	];
</script>

<Tabs>
	{#each tabs as { id, title, component, inputs }}
		<Tab {id} {title}>
			<svelte:component this={component} {...inputs} />
		</Tab>
	{/each}
</Tabs>
