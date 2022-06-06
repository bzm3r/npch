<script>
	import { class_titles, race_titles } from './CharacterData.svelte';
  //import { CharacterSummary } from './CharacterSummary.svelte';
	
	let race = "";
	let race_prompt = "First, pick a race:"
	let class1 = "";
	let class1_prompt = "Now, pick a companion/class:";
	let class2 = "";
	let class2_prompt = "Pick another companion/class:";
	let class3 = "";
	let class3_prompt = "Pick your last companion/class:";
	
	$: selectable_classes = class_titles.filter(class_title => class_title != class1 && class_title != class2 && class_title != class3);
</script>

<p>{race_prompt}</p>
<select bind:value={race} name="race" id="race-select">
	<option value={race}>{race}</option>
	{#each race_titles as race_title}
	<option value={race_title}>
		{race_title}
	</option>
	{/each}
</select>

{#if race != ""}
<p>{class1_prompt}</p>
<select bind:value={class1} name="class1" id="class1-select">
	<option value={class1}>{class1}</option>
	{#each selectable_classes as class_title}
	<option value={class_title}>
		{class_title}
	</option>
	{/each}
</select>
{/if}

{#if class1 != ""}
<p>{class2_prompt}</p>
<select bind:value={class2} name="class2" id="class2-select">
	<option value={class2}>{class2}</option>
	{#each selectable_classes as class_title}
	<option value={class_title}>
		{class_title}
	</option>
	{/each}
</select>
{/if}

{#if class2 != ""}
<p>{class3_prompt}</p>
<select bind:value={class3} name="class3" id="class3-select">
	<option value={class3}>{class3}</option>
	{#each selectable_classes as class_title}
	<option value={class_title}>
		{class_title}
	</option>
	{/each}
</select>
{/if}


