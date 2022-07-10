<script>
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';
	
	export const selectedTab = writable(0);
	
	setContext('selectedTab', selectedTab);
	
	let tabs = []; 
	
	setContext('registrar',{
		registerTab(id, title) {
			tabs = [...tabs, {id, title}];
		},
		unregisterTab(id) {
			tabs = tabs.filter(tab => tab.id != id);
		}
	});
	
	function selectTab(id) {
		$selectedTab = id;
	}

	let startX = 0;
	let endX = 0;

	function incrementSelectedTab() {
		if ($selectedTab === (tabs.length - 1)) {
			$selectedTab = 0;
		} else {
			$selectedTab += 1;
		}
	}

	function decrementSelectedTab() {
		if ($selectedTab === 0) {
			$selectedTab = tabs.length - 1;
		} else {
			$selectedTab -= 1;
		}
	}

	function swipeTab() {
		if (Math.abs(startX - endX) > 100) {
			if (startX < endX) {
				incrementSelectedTab()
			} else if (startX > endX) {
				decrementSelectedTab()
			}
		}
	}
	
	function onTouchStart(event) {
		startX = event.changedTouches[0].screenX;
	}

	function onTouchEnd(event) {
		endX = event.changedTouches[0].screenX;
		swipeTab();
	}

</script>

<div class="buttons">
	{#each tabs as {id, title}}
		<button class:active={$selectedTab === id} on:click={selectTab(id)}>
			{title}
		</button>
	{/each}
</div>

<div class="content" on:touchstart={onTouchStart} on:touchend={onTouchEnd}>
	<slot/>
</div>

<style>
	button.active {
		background: black;
		color: white;
	}
</style>
