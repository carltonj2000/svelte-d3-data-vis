<script lang="ts">
	import type { marginType, scaleType } from '../routes/+page.svelte';
	export let width: number;
	export let yScale: scaleType;
	export let margin: marginType;
	let yTicks = [0, 20, 40, 60];
</script>

<g transform="translate({margin.left} {margin.top})">
	{#each yTicks as tick, i}
		<text x={0} y={yScale(tick)} dy="-6"
			>{tick} {i == yTicks.length - 1 ? ' hours studied' : ''}</text
		>
		<line
			x1="0"
			y1={yScale(tick)}
			x2={width}
			y2={yScale(tick)}
			stroke={tick == 0 ? 'black' : '#a0a0a0'}
		/>
	{/each}
</g>
