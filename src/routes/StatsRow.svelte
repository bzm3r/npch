<script>
	import IconText from './IconText.svelte';

	export let primaries;
	export let totals;
</script>

<div class="container">
	{#each primaries as primary}
		<IconText id={primary} value={totals[primary].value} />
	{/each}
</div>

<style>
	.container {
		display: grid;
		width: 100%;
		grid-template-columns: repeat(4, 1fr);
		column-gap: 1em;
	}
</style>
