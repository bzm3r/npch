<script>
    import { primaries1, primaries2 } from './CharacterData.svelte';
    import IconText from './IconText.svelte';

    export let totals;
</script>

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

