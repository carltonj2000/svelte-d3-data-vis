<script lang="ts">
	import type { scaleType, studentType } from '../routes/+page.svelte';
	export let student: studentType;
	export let xScale: scaleType;
	export let yScale: scaleType;
</script>

<div class="tooltip" style="top: {yScale(student.hours)}px; left: {xScale(student.grade)}px">
	<h1>{student.name}</h1>
	<p>{student.hours} hours studied</p>
</div>

<style>
	.tooltip {
		position: absolute;
		padding: 0.25rem 1rem;
		background: rgba(255, 255, 255, 0.8);
		border: 1px solid rgba(0, 0, 0, 0.5);
		pointer-events: none;
		transition: top 300ms ease, left 300ms ease;
	}
	h1 {
		font-size: 20px;
	}
</style>

