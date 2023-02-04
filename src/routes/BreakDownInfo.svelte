<script>
	import { primaries1, primaries2, miscellaneous } from './CharacterData.svelte';

	export let id;
	export let value;

	let primaries = [...primaries1, ...primaries2];

	function calculateIconSrc(id) {
		if (id === 'special') {
			return '/special-star.svg';
		} else if (primaries.includes(id)) {
			return '/' + id + '.svg';
		} else if (miscellaneous.includes(id)) {
			if (id === 'Robotic') {
				return '';
			} else {
				return '/' + id.substring(0, id.length - 1).toLowerCase() + '.svg';
			}
		} else {
			return '';
		}
	}

	$: iconSrc = calculateIconSrc(id);
	$: console.log(id);
</script>

<div class="container">
	{#if iconSrc != ''}
		<img class="icon" src={iconSrc} alt={id + ' breakdown'} title={id + ' breakdown'} height="20" />
	{:else}
		<b class="icon">{id}</b>
	{/if}
	{#if id != 'special' && id != 'Charges' && id != 'Glands'}
		<p class="value">{value}</p>
	{/if}
</div>

<style>
	.container {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 0.2rem;
	}
</style>
