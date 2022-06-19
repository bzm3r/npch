<script>
	import { primaries1, primaries2, physicals, socials, knowledges, practicals, all_labels, races, classes } from './CharacterData.svelte';
	import IconText from './IconText.svelte';
	import SecondaryTables from './SecondaryTables.svelte';
	
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
		for (const label of all_labels) {
			totals[label] = 0;
			if (r_dat != null) {
				totals[label] += r_dat[label];
			}
			if (c1_dat != null) {
				totals[label] += c1_dat[label];
			}
			if (c2_dat != null) {
				totals[label] += c2_dat[label];
			}
			if (c3_dat != null) {
				totals[label] += c3_dat[label];
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
	<tr>
		{#each primaries1 as primary}
		<td>
			<IconText icon={primary} text={totals[primary]}></IconText>
		</td>
		{/each}
	</tr>
	<tr>
		{#each primaries2 as primary}
		<td>
			<IconText icon={primary} text={totals[primary]}></IconText>
		</td>
		{/each}
	</tr>
</table>

<SecondaryTables {totals}></SecondaryTables>

<p>
	Specials:
</p>
<ul>
		{#each specials as special}
				<li>{special}</li>
		{/each}
</ul>
