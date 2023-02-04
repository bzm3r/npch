<script>
	import { all_labels, miscellaneous, races, classes } from './CharacterData.svelte';
	import Stats from './Stats.svelte';
	import Skills from './Skills.svelte';
	import Other from './Other.svelte';
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

	class Breakdown {
		constructor(id) {
			this.id = id;
			this.partials = new Map();
			this.value = 0;
			this.special_id = '';
		}

		addNumeric(source, value) {
			if (value != 0) {
				this.partials.set(source, value);
				this.value += value;
			}
		}

		setSpecial(source, special) {
			if (special != '') {
				this.partials.set(source, 'special');
				this.value = special;
			}
			this.special_id = [...this.partials.keys()].concat(this.value).join('').replaceAll(' ', '');
		}

		setSpecialMultiSource(sources, special) {
			if (special != '') {
				console.log(sources);
				sources.forEach((source) => this.partials.set(source, 'special'));
				this.value = special;
			}
			this.special_id = [...this.partials.keys()].concat(this.value).join('').replaceAll(' ', '');
		}
	}

	function updateTotals(r_dat, c1_dat, c2_dat, c3_dat) {
		let totals = new Map();
		for (const label of all_labels) {
			totals[label] = new Breakdown(label);
			if (r_dat != null) {
				totals[label].addNumeric(r_dat.title, r_dat[label]);
			}
			if (c1_dat != null) {
				if (r_dat != null && r_dat.title === 'Human-Academic' && !miscellaneous.includes(label)) {
					totals[label].addNumeric(c1_dat.title, 2 * c1_dat[label]);
				} else {
					totals[label].addNumeric(c1_dat.title, c1_dat[label]);
				}
			}
			if (c2_dat != null) {
				totals[label].addNumeric(c2_dat.title, c2_dat[label]);
			}
			if (c3_dat != null) {
				totals[label].addNumeric(c3_dat.title, c3_dat[label]);
			}
		}
		return totals;
	}

	$: totals = updateTotals(r_dat, c1_dat, c2_dat, c3_dat);

	function createSpecialBreakdowns(source, specials) {
		if (!Array.isArray(source)) {
			return specials.map((special) => {
				let breakdown = new Breakdown('special');
				breakdown.setSpecial(source, special);
				return breakdown;
			});
		} else {
			return specials.map((special) => {
				let breakdown = new Breakdown('special');
				breakdown.setSpecialMultiSource(source, special);
				return breakdown;
			});
		}
	}

	function getSpecials(r_dat, c1_dat, c2_dat, c3_dat) {
		let primary_specials = [];
		let skill_specials = [];
		let flavor_specials = [];
		let equipment = [];
		[r_dat, c1_dat, c2_dat, c3_dat].forEach((dat) => {
			if (dat != null) {
				primary_specials.push(...createSpecialBreakdowns(dat.title, dat.specials.primary));
				skill_specials.push(...createSpecialBreakdowns(dat.title, dat.specials.skill));
				flavor_specials.push(...createSpecialBreakdowns(dat.title, dat.specials.flavor));
				equipment.push(...createSpecialBreakdowns(dat.title, dat.specials.equipment));
			}
		});

		if (r_dat != null && r_dat.title === 'Human-Academic') {
			if (c1_dat != null) {
				primary_specials.push(
					...createSpecialBreakdowns([r_dat.title, c1_dat.title], c1_dat.specials.primary)
				);
				skill_specials.push(
					...createSpecialBreakdowns([r_dat.title, c1_dat.title], c1_dat.specials.skill)
				);
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
			id: 1,
			title: 'Skills',
			component: Skills,
			inputs: { totals: totals, specials: skill_specials }
		},
		{
			id: 0,
			title: 'Stats',
			component: Stats,
			inputs: { totals: totals, specials: primary_specials }
		},
		{
			id: 2,
			title: 'Other',
			component: Other,
			inputs: { flavor_specials: flavor_specials, equipment: equipment }
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
