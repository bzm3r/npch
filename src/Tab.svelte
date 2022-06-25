<script>
	import { getContext, onMount, onDestroy } from 'svelte';
	
	export let id;
	export let title;
	
	let selectedTab = getContext('selectedTab');
	const registrar = getContext('registrar');
	
	onMount(() => {
		registrar.registerTab(id, title);
	});
	
	onDestroy(() => {
		registrar.unregisterTab(id);
	});
</script>

{#if $selectedTab === id}
	<slot/>
{/if}
