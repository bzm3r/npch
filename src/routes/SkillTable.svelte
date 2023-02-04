<script>
	export let totals;
	export let labels = [];

	import { getContext } from 'svelte';
	const currentFocus = getContext('currentFocus');

	function handleClick(label) {
		if ($currentFocus === label) {
			$currentFocus = '';
		} else {
			$currentFocus = label;
		}
	}
</script>

<table>
	{#each labels as label}
		<tr
			style={$currentFocus === label ? 'background-color: gold;' : ''}
			on:click={() => handleClick(label)}
		>
			<th>{label}</th>
			<td>{totals[label].value}</td>
		</tr>
	{/each}
</table>

<style>
	table {
		outline-style: solid;
		width: 10rem;
	}

	tr:nth-of-type(odd) {
		background-color: #ccc;
	}

	td {
		text-align: center;
		width: 10%;
	}

	th {
		width: 90%;
	}

	tr {
		height: 1rem;
	}
</style>
