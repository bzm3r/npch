<script>
	export let totals;
	export let labels = [];
</script>

<table>
	{#each labels as label}
		<tr>
			<th>{label}</th>
			<td>{totals[label]}</td>
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
	}

	th {
		width: 90%;
	}

	tr {
		width: 10%;
	}
</style>
