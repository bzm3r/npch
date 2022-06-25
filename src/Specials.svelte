<script>
    export let specials;
</script>

<p>
	Specials:
</p>
<ul>
		{#each specials as special}
				<li>{special}</li>
		{/each}
</ul>
