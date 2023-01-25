<script>
	export let specials;
</script>

<div class="container">
	<ul>
		{#each specials as special}
			<li>{special}</li>
		{/each}
	</ul>
</div>

<style>
	.container {
		width: 300px;
	}
</style>
