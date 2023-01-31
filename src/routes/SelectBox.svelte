<script>
	export let name = '';
	export let choices = [];
	export let selected = '';
	export let html_class = '';
</script>

<select bind:value={selected} {name} id={name} class={html_class}>
	<option value="" />
	{#each choices as choice}
		<option value={choice}>{choice}</option>
	{/each}
</select>

<style>
	select {
		width: 50%;
	}
	.human_academic {
		border-color: black;
		border-width: 0.3rem;
		border-style: solid;
		border-radius: 0.2rem;
	}
</style>
