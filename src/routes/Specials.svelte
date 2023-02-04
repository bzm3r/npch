<script>
	export let specials;
	export let heading = '';

	import { getContext } from 'svelte';
	const currentFocus = getContext('currentFocus');

	function setFocus(id) {
		if ($currentFocus === id) {
			$currentFocus = '';
		} else {
			$currentFocus = id;
		}
	}
</script>

<div class="container">
	{#if heading != ''}
		<h4>{heading}</h4>
	{/if}
	<ul>
		{#each specials as special}
			<li
				on:click={() => setFocus(special.special_id)}
				on:keydown={() => setFocus(special.special_id)}
				style={$currentFocus === special.special_id ? 'background-color: gold;' : ''}
			>
				{special.value}
			</li>
		{/each}
	</ul>
</div>
