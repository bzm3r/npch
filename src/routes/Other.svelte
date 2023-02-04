<script>
	import Specials from './Specials.svelte';

	export let flavor_specials;
	export let equipment;

	import { setContext, getContext } from 'svelte';
	import { writable } from 'svelte/store';

	const currentFocus = writable('');

	setContext('currentFocus', currentFocus);

	const currentBreakdown = getContext('currentBreakdown');
	function fetchBreakdown(id) {
		if (id) {
			let breakdown = flavor_specials.find((special) => special.special_id === id);
			if (breakdown) {
				return breakdown;
			} else {
				return equipment.find((special) => special.special_id === id);
			}
		} else {
			return null;
		}
	}
	$: $currentBreakdown = fetchBreakdown($currentFocus);
</script>

{#if flavor_specials.length > 0}
	<Specials heading="Specials" specials={flavor_specials} />
{/if}

{#if equipment.length > 0}
	<Specials heading="Equipment" specials={equipment} />
{/if}
