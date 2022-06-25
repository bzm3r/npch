<script>
	export let title = "";
	export let name = "";
	export let choices = [];
	export let selected = "";
</script>


<tr>
	<th>{title}: </th>
	<td>
		<select bind:value={selected} {name} id={name}>
			{#if selected != ""}
				<option value=""></option>
			{/if}
			<option value={selected}>{selected}</option>
			{#each choices as choice}
				<option value={choice}>{choice}</option>
			{/each}
		</select>
	</td>
</tr>
