<script>
	import CharacterSummary from './CharacterSummary.svelte';
	import SelectBoxes from './SelectBoxes.svelte';
	
	let race = "";
	let class1 = "";
	let class2 = "";
	let class3 = "";
</script>

<!-- <div class="header-img">
	<img class="header-pic" src="/assets/header.webp" alt="city on a planet's darkside" height=350px>
</div> -->

<SelectBoxes bind:race={race} bind:class1={class1} bind:class2={class2} bind:class3={class3}></SelectBoxes>

<CharacterSummary {race} {class1} {class2} {class3}>
</CharacterSummary>

<style>
	.header-img {
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.header-img::before {
		background: linear-gradient(to bottom, rgba(255, 255, 255, 0.0), rgba(255, 255, 255, 1.0));	
	}
</style>