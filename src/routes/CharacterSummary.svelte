<script>
	import { all_labels, primaries3, races, classes } from './CharacterData.svelte';
	import Primaries from './Primaries.svelte';
	import Secondaries from './Secondaries.svelte';
	import Specials from './Specials.svelte';
	import Tabs from './Tabs.svelte';
	import Tab from './Tab.svelte';

	export let race = '';
	export let class1 = '';
	export let class2 = '';
	export let class3 = '';

	$: r_dat = race != '' ? races.get(race) : null;
	$: c1_dat = class1 != '' ? classes.get(class1) : null;
	$: c2_dat = class2 != '' ? classes.get(class2) : null;
	$: c3_dat = class3 != '' ? classes.get(class3) : null;

	function calculateTotals(r_dat, c1_dat, c2_dat, c3_dat) {
		let totals = new Map();
		for (const label of all_labels) {
			totals[label] = 0;
			if (r_dat != null) {
				totals[label] += r_dat[label];
			}
			if (c1_dat != null) {
				if (r_dat != null && r_dat.title === 'Human-Academic' && !primaries3.includes(label)) {
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
		return totals;
	}

	$: totals = calculateTotals(r_dat, c1_dat, c2_dat, c3_dat);

	function getSpecials(r_dat, c1_dat, c2_dat, c3_dat) {
		let primary_specials = [];
		let skill_specials = [];
		let flavor_specials = [];
		let equipment = [];
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

		return [primary_specials, skill_specials, flavor_specials, equipment];
	}

	$: [primary_specials, skill_specials, flavor_specials, equipment] = getSpecials(
		r_dat,
		c1_dat,
		c2_dat,
		c3_dat
	);
	
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
