<script lang="ts">
	import type { marginType, scaleType } from '../routes/+page.svelte';
	export let height: number;
	export let xScale: scaleType;
	export let margin: marginType;
	let xTicks = [0, 25, 50, 75, 100];
</script>

<g>
	{#each xTicks as tick}
		<text x={xScale(tick)} y={height - margin.bottom} dominant-baseline="hanging" dy="6"
			>{tick}%</text
		>
	{/each}
</g>
