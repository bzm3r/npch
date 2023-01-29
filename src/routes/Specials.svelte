<script>
	export let specials;
	export let heading = '';
</script>

<div class="container">
	{#if heading != ''}
		<h4>{heading}</h4>
	{/if}
	<ul>
		{#each specials as special}
			<li>{special}</li>
		{/each}
	</ul>
</div>
