<script>
	import { scaleLinear, scaleSqrt } from "d3-scale";
  import { extent, min, max } from "d3-array";
  import { tweened } from "svelte/motion";
  import { cubicOut } from "svelte/easing";
	
  export let step;

	// elevation levels updated on scroll
  let elevations = [
    { high: 500, medium: 300, low: 100 },
  ];

  let width;
  let height;

  const margin = { top: 30, bottom: 30, left: 30, right: 30 };

  const tweenOptions = {
    delay: 0,
    duration: 1000,
    easing: cubicOut,
  };

  const tweenedY = tweened(
    elevations.map((d) => d.high),
    tweenOptions
  );

  $: tweenedData = elevations.map((d, index) => ({
    y: $tweenedY[index]
  }));

  function setTween(elevation, key) {
    elevation.set(elevations.map((d) => +d[key]));
  }

  $: {
    if (step == 0) {
      setTween(tweenedY, "high");
    }
    if (step == 1) {
      setTween(tweenedY, "medium");
    }
    if (step == 2) {
      setTween(tweenedY, "low");
    }
  }

  $: yScale = scaleLinear()
    .domain(extent($tweenedY, (d) => d))
    .range([height - margin.top, margin.bottom]);
</script>

<div
  class="chart-container"
  bind:offsetWidth={width}
  bind:offsetHeight={height}
>
  <svg class="water" width={width + margin.right + margin.left} {height}>
		{#each tweenedData as d}
			<rect
					x={0}
					y={height - d.y}
					width={width}
					height={d.y}
					fill="steelblue"
					opacity=".9"
				/>
		{/each}
  </svg>
	
	<svg class ="triangle-left" viewBox="0 0 20 100">
    <polygon points="0,0 0,100 80,500" />
  </svg>

  <svg class ="triangle-right" viewBox="0 0 20 100">
    <polygon points="20,0 20,100 0,150" />
  </svg>
	
</div>

<style>
  .chart-container {
		position: relative;
		margin: 10px;
    height: 90vh;
    max-width: 100%;
		background: skyblue;
		border-radius: 5px;
  }
	
	.water {
		border-radius: 5px;
	}
	
	.triangle-left {
		position: absolute;
		top: auto;
		bottom: 0;
		left: 0;
		height: 80vh;
		fill: #D4AB6D;
		border-radius: 5px;
	}

	.triangle-right {
		position: absolute;
		bottom: 0;
		right: 0; 
		height: 80vh;
		fill: #D4AB6D;
		border-radius: 5px;
	}
</style>