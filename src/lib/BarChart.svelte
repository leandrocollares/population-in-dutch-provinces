<script>
  import * as d3 from 'd3';

  export let data;

  const formatLabel = d3.format(',.0f');

  const xAccessor = d => +d.population;
  const yAccessor = d => d.province;

  const margin = {
    top: 30,
    right: 75,
    bottom: 0,
    left: 110,
  };

  let width = 400;
  let height = 500;

  $: innerWidth = width - margin.left - margin.right;
  let innerHeight = height - margin.top - margin.bottom;

  $: xScale = d3
    .scaleLinear()
    .domain([0, d3.max(data, xAccessor)])
    .range([0, innerWidth]);

  const yScale = d3
    .scaleBand()
    .domain(data.map(d => d.province))
    .range([innerHeight, 0])
    .padding(0.25);

  $: xAccessorScaled = d => xScale(xAccessor(d));
  $: yAccessorScaled = d => yScale(yAccessor(d));
</script>

<div class="wrapper" bind:clientWidth={width}>
  <svg class="chart" {width} {height}>
    <g transform={`translate(${margin.left}, ${margin.top})`}>
      {#each data as d}
        <text
          text-anchor="end"
          x={-10}
          y={yScale(d.province) + yScale.bandwidth() / 2}
          dy=".32em"
        >
          {d.province}
        </text>
        <rect
          x={0}
          y={yAccessorScaled(d)}
          width={xAccessorScaled(d)}
          height={yScale.bandwidth()}
        />
        <text
          text-anchor="start"
          x={xScale(xAccessor(d))}
          dx="10"
          y={yScale(d.province) + yScale.bandwidth() / 2}
          dy=".32em"
        >
          {formatLabel(d.population)}
        </text>
      {/each}
    </g>
  </svg>
</div>

<style>
  .wrapper {
    position: relative;
    width: 100%;
    max-width: 700px;
  }

  rect {
    fill: #ff4941;
  }
</style>
