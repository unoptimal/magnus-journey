<script>
    export let step;
  
    let data = {
      one: [
        { year: 1999, value: 904 },
        { year: 2000, value: 1907 },
        { year: 2001, value: 2084 },
        { year: 2002, value: 2250  },
        { year: 2003, value: 2450 },
      ],
      two: [
        { year: 2004, value: 2581 },
        { year: 2005, value: 2570 },
        { year: 2006, value: 2698 },
        { year: 2007, value: 2714  },
        { year: 2008, value: 2786 },
      ],
      three: [
        { year: 2009, value: 2801  },
        { year: 2010, value: 2802 },
        { year: 2011, value: 2826 },
        { year: 2012, value: 2848  },
        { year: 2013, value: 2872  },
      ],
      four: [
        { year: 2014, value: 2882 },
        { year: 2015, value: 2850 },
        { year: 2016, value: 2840 },
        { year: 2017, value: 2837  },
        { year: 2018, value: 2842 },
      ],
      five: [
        { year: 2019, value: 2882 },
        { year: 2020, value: 2863  },
        { year: 2021, value: 2855 },
        { year: 2022, value: 2859  },
        { year: 2023, value: 2853 },
      ],
    };
  
    import { scaleLinear, scaleSqrt } from "d3-scale";
    import { extent, min, max } from "d3-array";
    import { tweened } from "svelte/motion";
    import { cubicOut } from "svelte/easing";
  
    let width;
    let height;
  
    const margin = { top: 30, bottom: 30, left: 30, right: 30 };
  
    const tweenOptions = {
      delay: 0,
      duration: 1000,
      easing: cubicOut,
    };
  
    let currentData = data.one;
  
    const tweenedX = tweened(
      currentData.map((d) => d.year),
      tweenOptions
    );
  
    const tweenedY = tweened(
      currentData.map((d) => d.value),
      tweenOptions
    );
  
    $: tweenedData = currentData.map((d, index) => ({
      x: $tweenedX[index],
      y: $tweenedY[index]
    }));
  
    function setTween(dimension, key) {
      currentData = data[key];
      dimension.set(currentData.map((d) => d.year));
      tweenedY.set(currentData.map((d) => d.value));
    }
  
    $: {
      if (step == 0) {
        setTween(tweenedX, "one");
      }
      if (step == 1) {
        setTween(tweenedX, "two");
      }
      if (step == 2) {
        setTween(tweenedX, "three");
      }
      if (step == 3) {
        setTween(tweenedX, "four");
      }
      if (step == 4) {
        setTween(tweenedX, "five");
      }
    }

    $: xScale = scaleLinear()
      .domain(extent($tweenedX, (d) => d))
      .range([margin.left, width - margin.right]);
  
    $: yScale = scaleLinear()
      .domain([1900,2900])
      .range([height - margin.top, margin.bottom]);
  
    const numTicks = 5; // Number of tick marks
  
    $: xTicks = xScale.ticks(numTicks);
    $: yTicks = yScale.ticks(numTicks);
  
    let tooltipValue = null;
  
    function handleMouseOver(event, d) {
      tooltipValue = d;
    }
  
    function handleMouseOut() {
      tooltipValue = null;
    }
  </script>
  
  <div class="chart-container" bind:offsetWidth={width} bind:offsetHeight={height}>
    <svg width={width + margin.right + margin.left} {height}>
      
      <!-- X-axis tick marks and labels -->
      {#each xTicks as tick}
        <line
          x1={xScale(tick)}
          y1={height - margin.bottom}
          x2={xScale(tick)}
          y2={height - margin.bottom + 6}
          stroke="black"
        />
        <text
          x={xScale(tick)}
          y={height - margin.bottom + 20}
          text-anchor="middle"
          font-size="10px"
          fill="black"
        >
          {tick}
        </text>
      {/each}
  
      <!-- Y-axis label -->
      <text
        x={width / 2}
        y={margin.top / 2 + 15}
        text-anchor="middle"
        font-size="18px"
        fill="black"
      >
        Carlsen's Rating Over Time
      </text>
  
      <!-- Y-axis tick marks and labels -->
      {#each yTicks as tick}
        <line
          x1={margin.left}
          y1={yScale(tick)}
          x2={margin.left}
          y2={yScale(tick)}
          stroke="black"
        />
        <text
          x={margin.left + 10}
          y={yScale(tick)}
          text-anchor="end"
          alignment-baseline="middle"
          font-size="10px"
          fill="black"
        >
          {tick}
        </text>
      {/each}
  
      {#each tweenedData as d}
        <circle
          cx={xScale(d.x)}
          cy={yScale(d.y)}
          r={5}
          fill="#000000"
          stroke="#FFFFFF"
          opacity=".9"
          on:mouseover={(e) => handleMouseOver(e, d)}
          on:mouseout={handleMouseOut}
        />
      {/each}
    </svg>
  
    {#if tooltipValue}
      <div class="tooltip">
        <p>Rating: {tooltipValue.y}</p>
      </div>
    {/if}
  </div>
  
  <style>
    .chart-container {
      height: 80vh;
      max-width: 100%;
      background: linear-gradient(to bottom left, #769656 -10%, white 100%);
      border-radius: 5px;
      box-shadow: 1px 1px 6px #cecece;
      position: relative;
    }
  
    .tooltip {
      position: absolute;
      top: 10px;
      right: 10px;
      padding: 5px;
      background-color: rgba(0, 0, 0, 0.8);
      color: white;
      font-size: 12px;
      pointer-events: none;
    }
  </style>
  