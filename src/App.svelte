<script lang="ts">
	import { quintInOut, sineIn } from 'svelte/easing';

	import { tweened } from 'svelte/motion';
	let x = false;
	const deltaY = tweened(0, {
		duration: 500,
		easing: quintInOut,
		delay: 0,

	});
	const deltaX = tweened(1, {
		duration: 500,
		easing: quintInOut,
		delay: 0,
	});
	function handleClick() {
		if (!x) {
			if ($deltaX === 1) $deltaX = 0;
			if ($deltaY === 0) $deltaY = 1;
		} else {
			if ($deltaY === 1) $deltaY = 0;
			if ($deltaX === 0) $deltaX = 1;
		}
		x = !x;
	}
	$: console.log(22 - 22 * $deltaY);
</script>

<main>
	<svg
		on:click={handleClick}
		width="25"
		height="25"
		xmlns="http://www.w3.org/2000/svg"
	>
		<line
			x1="1"
			x2="24"
			y1="2"
			y2={25 * $deltaY + ($deltaY  < .5 ? 2 : -2)}
			stroke="black"
			stroke-width="4"
		/>
		<line
			x1="1"
			x2={23 * $deltaX + 1}
			y1="12"
			y2="12"
			stroke="black"
			stroke-width="4"
		/>
		<line
			x1="1"
			x2="24"
			y1="23"
			y2={25 * $deltaX + ($deltaX  < .5 ? 3 : -2)}
			stroke="black"
			stroke-width="4"
		/>
	</svg>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}
	svg {
		/* border: 1px solid red; */
		/* border-radius: 8px; */
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>
