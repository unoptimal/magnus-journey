<script>
	import chartjs from 'chart.js/auto';
	import { onMount } from 'svelte';

	let ctx;
	let chartCanvas;

	onMount(async (promise) => {
      fetch(`magnus_carlsen_ratings.json`)
      .then(response => response.json())
        .then(data => {
		  ctx = chartCanvas.getContext('2d');
			var chart = new chartjs(ctx, {
				type: 'line',
				data: {
                    labels: data.slice().reverse().map(d => d.date),
                    datasets: [{
                    label: 'Rating',
                    data: data.slice().reverse().map(d => d.standard),
                    fill: false,
                    borderColor: 'rgb(75, 192, 192)',
                    tension: 0.1
						}]
				},
                options: {
                responsive: true,
                scales: {
                    x: {
                        title: {
                            display: true,
                            text: 'Year-Month'
                        },
                        grid:{
                            display: false
                        }
                        
                    },
                    y: {
                        title: {
                            display: true,
                            text: 'Rating'
                        },
                        grid:{
                            display: false
                        }
                    }
                }
            }
		});

	});
    });
</script>

<canvas bind:this={chartCanvas} id="myChart"></canvas>
