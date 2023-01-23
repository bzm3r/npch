<script>
    export let specials;
</script>

<ul>
	{#each specials as special}
		<li>{special}</li>
	{/each}
</ul>
