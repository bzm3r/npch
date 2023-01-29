<script>
	import Specials from './Specials.svelte';

	export let flavor_specials;
	export let equipment;
</script>

{#if flavor_specials.length > 0}
	<Specials heading="Specials" specials={flavor_specials} />
{/if}

{#if equipment.length > 0}
	<Specials heading="Equipment" specials={equipment} />
{/if}
