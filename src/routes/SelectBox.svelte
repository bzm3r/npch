<script>
	export let name = '';
	export let choices = [];
	export let selected = '';
	export let html_class = '';
</script>

<select bind:value={selected} {name} id={name} class={html_class}>
	{#if selected != ''}
		<option value="" />
	{/if}
	<option value={selected}>{selected}</option>
	{#each choices as choice}
		<option value={choice}>{choice}</option>
	{/each}
</select>

<style>
	select {
		width: 200px;
	}
	.human_academic {
		border-color: black;
		border-width: 5px;
		border-style: solid;
		border-radius: 2px;
	}
</style>
