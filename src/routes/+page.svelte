<script lang="ts">
	import students from '../data/data.js';
	import { scaleLinear } from 'd3-scale';
	import { max } from 'd3-array';

	let width = 400;
	let height = 400;

	const xScale = scaleLinear().domain([0, 110]).range([0, width]);
	const yScale = scaleLinear()
		.domain([0, max(students, (s) => s.hours) + 10])
		.range([height, 0]);
</script>

<svg {width} {height}>
	{#each students as { grade, hours }}
		<circle cx={xScale(grade)} cy={yScale(hours)} r="10" fill="purple" stroke="yellow" />
	{/each}
</svg>

