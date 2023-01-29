<script>
	import './styles.css';

	import CharacterSummary from './CharacterSummary.svelte';
	import CharacterSelect from './CharacterSelect.svelte';
	import PrintButton from './PrintButton.svelte';

	let race = '';
	let class1 = '';
	let class2 = '';
	let class3 = '';
</script>

<svelte:head>
	<title>NPCH Character Calculator</title>
	<meta name="description" content="NPCH Character Calculator" />
</svelte:head>

<!-- <div class="header-img">
	<img class="header-pic" src="/assets/header.webp" alt="city on a planet's darkside" height=350px>
</div> -->

<div class="main_container">
	<div class="character_select">
		<CharacterSelect bind:race bind:class1 bind:class2 bind:class3 />
	</div>

	<div class="character_summary">
		<CharacterSummary {race} {class1} {class2} {class3} />
	</div>

	<div class="print_button">
		<PrintButton {race} {class1} {class2} {class3} />
	</div>

	<div class="other_links">
		<a href="https://github.com/bzm3r/npch/issues">Report issues</a>
	</div>
</div>

<style>
	.main_container {
		display: grid;
		grid-auto-flow: row;
		margin: 0 auto;
		justify-content: center;
		justify-items: center;
		row-gap: 1rem;
		/* border-color: black;
		border-width: 1px;
		border-style: solid; */
	}

	.character_select {
		width: 25rem;
		grid-area: 'character_select';
		/* border-color: red;
		border-width: 1px;
		border-style: solid; */
	}

	.character_summary {
		width: 20rem;
		grid-area: 'character_summary';
		/* border-color: blue;
		border-width: 1px;
		border-style: solid; */
	}

	/* .header-img {
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.header-img::before {
		background: linear-gradient(to bottom, rgba(255, 255, 255, 0.0), rgba(255, 255, 255, 1.0));	
	} */
</style>
