<script>
	export let value;
	export let id;

	import { getContext } from 'svelte';
	const currentFocus = getContext('currentFocus');

	function handleClick() {
		if ($currentFocus === id) {
			$currentFocus = '';
		} else {
			$currentFocus = id;
		}
	}

	$: focusedText = $currentFocus === id ? ' focused' : '';

	let src = '/' + id + '.svg';

	let iconY = {
		atk: 65,
		def: 60,
		fort: 60,
		hp: 65,
		init: 90,
		ref: 60,
		skl: 60,
		will: 60
	};
	let iconX = {
		atk: 50,
		def: 50,
		fort: 55,
		hp: 50,
		init: 55,
		ref: 50,
		skl: 40,
		will: 50
	};
</script>

<div class="iconButton" on:click={handleClick} on:keypress={handleClick}>
	<p class="screen-reader-description">{id}</p>
	<img class={'iconImage' + focusedText} {src} alt={id + focusedText} title={id} />
	<div class="iconValue" style:--y="-{iconY[id]}%" style:--x="-{iconX[id]}%">
		{value}
	</div>
</div>

<style>
	.iconButton {
		outline: none;
		background-color: transparent;
		border: 0cap;
		position: relative;
		text-align: center;
		color: black;
	}

	.iconImage {
		z-index: 0;
	}

	.iconValue {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(var(--x), var(--y));
		z-index: 1;
		font-weight: bold;
	}

	.focused {
		background-color: gold;
	}

	.screen-reader-description {
		border: 0;
		clip: rect(0 0 0 0);
		height: 1px;
		margin: -1px;
		overflow: hidden;
		padding: 0;
		position: absolute;
		white-space: nowrap;
		width: 1px;
	}
</style>
