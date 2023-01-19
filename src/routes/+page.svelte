<script lang="ts" context="module">
	export type marginType = { top: number; right: number; left: number; bottom: number };
	export type scaleType = (i: number) => number;
	export type studentType = { name: string; grade: number; hours: number };
	export type studentsType = studentType[];
</script>

<script lang="ts">
	import data from '../data/data.js';
	import { scaleLinear } from 'd3-scale';
	import { max } from 'd3-array';
	import AxisX from '../components/AxisX.svelte';
	import AxisY from '../components/AxisY.svelte';
	import Tooltip from '../components/Tooltip.svelte';

	let width = 400;
	let height = 400;
	let margin: marginType = { top: 20, right: 40, left: 0, bottom: 20 };

	let students: studentsType = data.sort((a, b) => (a.grade > b.grade ? 1 : -1));
	$: xScale = scaleLinear()
		.domain([0, 100])
		.range([0, width - margin.left - margin.right]);
	const yScale = scaleLinear()
		.domain([0, max(students, (s) => s.hours) || 0])
		.range([height - margin.top - margin.bottom, 0]);

	let hoveredData: studentType | null = null;
</script>

<h1>Study Long, Score Better</h1>
<div class="chart-container" bind:clientWidth={width} on:mouseleave={() => (hoveredData = null)}>
	<svg {width} {height}>
		<AxisX {height} {xScale} {margin} />
		<AxisY {width} {yScale} {margin} />
		<g class="circles" transform="translate({margin.left} {margin.top})">
			{#each students as student}
				<circle
					cx={xScale(student.grade)}
					cy={yScale(student.hours)}
					r={hoveredData == student ? 20 : '10'}
					fill="purple"
					stroke="yellow"
					opacity={hoveredData ? (hoveredData == student ? 1 : 0.5) : 1}
					on:mouseover={() => {
						hoveredData = student;
					}}
					on:focus={() => {
						hoveredData = student;
					}}
					tabIndex="0"
				/>
			{/each}
		</g>
	</svg>
	{#if hoveredData}
		<Tooltip student={hoveredData} {xScale} {yScale} />
	{/if}
</div>

<style>
	circle {
		transition: r 300ms ease, opacity 300ms ease;
		cursor: pointer;
	}
	circle:focus {
		outline: none;
	}
</style>
