<script>
	import { onMount } from 'svelte';
	import * as d3 from 'd3';
	import { scaleLinear } from 'd3-scale';
	import { interpolateRainbow } from 'd3';

	onMount(() => {
		const scale = 0.4;
		const margin = { top: -20, right: 10, bottom: 10, left: 10 };
		// const width = scale * 500 - margin.left - margin.right;
		// const height = scale * 500 - margin.top - margin.bottom;
		const width = 200;
		const height = 100;
		const amp = 3;
		const x_amp = amp * 1;
		const y_amp = amp * 0.3;
		const x_freq = 1;
		const y_freq = 2;
		const svg = d3
			.select('#scatter_area')
			.attr('width', width + margin.left + margin.right)
			.attr('height', height + margin.top + margin.bottom)
			.append('g')
			.attr('transform', `translate(${margin.left},${margin.top})`);

		const x = scaleLinear().domain([-Math.PI, Math.PI]).range([0, width]);
		const y = scaleLinear().domain([-Math.PI, Math.PI]).range([height, 0]);
		const col_scale = scaleLinear()
			.domain([0, 2 * Math.PI])
			.range([0, 1]);

		const npoints = 150;
		const range = Array.from(Array(npoints).keys());
		const range_pi = range.map((j) => ((2 * j) / npoints) * Math.PI - Math.PI);
		// var data = range.map((e) => ({ n: e, pi: range_pi[e], col: col_scale(range_pi[e]) }));
		const col_offset = Math.PI;
		var data = range.map((e) => ({
			n: e,
			pi: range_pi[e],
			col: col_scale(range_pi[e] + col_offset)
		}));

		const stdev = 2;
		const thing1 = 51;
		const thing2 = -14;
		const color_mat = '1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 ' + thing1 + ' ' + thing2;

		var filter = svg.append('filter').attr('id', 'gooeyCodeFilter');
		filter
			.append('feGaussianBlur')
			.attr('in', 'SourceGraphic')
			.attr('stdDeviation', stdev)
			.attr('color-interpolation-filters', 'sRGB')
			.attr('result', 'blur');
		filter
			.append('feColorMatrix')
			.attr('class', 'blurValues')
			.attr('in', 'blur')
			.attr('mode', 'matrix')
			.attr('values', color_mat)
			.attr('result', 'gooey');
		filter.append('feBlend').attr('in', 'blur').attr('in2', 'gooey').attr('operator', 'atop');

		function circleTransition() {
			let points_wrapper = svg
				.append('g')
				// .style('filter', 'url(#gooeyCodeFilter)') // Applying the filter here

				.selectAll('points')
				.data(data)
				.enter()
				.append('circle')
				.attr('id', (d) => d['n'])
				.attr('pi', (d) => d['pi'])
				.style('fill', (d) => interpolateRainbow(d['col']))
				.attr('r', '5');
			// .style('opacity', 0.5)

			function repeat() {
				points_wrapper
					.transition()
					.duration(4000)
					.attrTween('cx', function () {
						return function (t) {
							let offset = parseFloat(this.getAttribute('pi'));
							return x(x_amp * Math.cos(x_freq * (t * 2 * Math.PI) + offset));
						};
					})
					.attrTween('cy', function () {
						return function (t) {
							let offset = parseFloat(this.getAttribute('pi'));
							return y(y_amp * Math.sin((y_freq * (t * 2 * Math.PI) + offset) * 2));
						};
					})
					.attrTween('r', function () {
						return function (t) {
							const offset = parseFloat(this.getAttribute('pi'));
							return 2 * (Math.cos(t * 2 * Math.PI + offset + Math.PI) + Math.PI);
						};
					});
			}
			repeat();
		}
		circleTransition();
	});
</script>

<svg id="scatter_area" />

<style>
	#scatter_area {
		filter: url(#gooeyCodeFilter);
	}
</style>
