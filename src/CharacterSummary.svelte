<script>
	import { stat_labels, races, classes } from './CharacterData.svelte';
	
	export let race = "";
	export let class1 = "";
	export let class2 = "";
	export let class3 = "";
	
	let r_dat = null;
	let c1_dat = null;
	let c2_dat = null;
	let c3_dat = null;
	
	let titles = [];
	let totals = new Map();
	stat_labels.forEach(stat => totals.set(stat, 0));
	let specials = [];
	
	function updateTitles(r_dat, c1_dat, c2_dat, c3_dat) {
		titles = [];
		[r_dat, c1_dat, c2_dat, c3_dat].forEach(dat => {if (dat != null) {
			titles.push(dat.title);
		}})
	}
	
	function updateSpecials(r_dat, c1_dat, c2_dat, c3_dat) {
		specials = [];
		[r_dat, c1_dat, c2_dat, c3_dat].forEach(dat => {if (dat != null) {
			specials.push(...dat.specials);
		}})
	}
	
	function updateTotals(r_dat, c1_dat, c2_dat, c3_dat) {
		for (const stat of stat_labels) {
			totals[stat] = 0;
			if (r_dat != null) {
				totals[stat] += r_dat[stat];
			}
			if (c1_dat != null) {
				totals[stat] += c1_dat[stat];
			}
			if (c2_dat != null) {
				totals[stat] += c2_dat[stat];
			}
			if (c3_dat != null) {
				totals[stat] += c3_dat[stat];
			}
		}
	}
	
	$: if (race != "") {
		r_dat = races.get(race);
	} else {
		r_dat = null;
	}
	$: if (class1 != "") {
		c1_dat = classes.get(class1);
	} else {
		c1_dat = null;
	}
	$: if (class2 != "") {
		c2_dat = classes.get(class2);
	} else {
		c2_dat = null;
	}
	$: if (class3 != "") {
		c3_dat = classes.get(class3);
	} else {
		c2_dat = null;
	}
	$: updateTitles(r_dat, c1_dat, c2_dat, c3_dat);
	$: updateSpecials(r_dat, c1_dat, c2_dat, c3_dat);
	$: updateTotals(r_dat, c1_dat, c2_dat, c3_dat);
</script>

<p>
	{titles.join(" + ")}
</p>

<table>
	{#each stat_labels as stat}
	<tr>
		<th>{stat}</th>
		<td>{totals[stat]}</td>
	</tr>
	{/each}
</table>

<p>
	Specials:
</p>
<ul>
		{#each specials as special}
				<li>{special}</li>
		{/each}
</ul> 


