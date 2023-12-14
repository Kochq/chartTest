<script>
    import { onMount, onDestroy } from 'svelte';
    import Chart from 'chart.js/auto';

    export let chartData;
    export let id;

    let chart;

    onMount(() => {
        const ctx = document.getElementById(id);

        // @ts-ignore
        chart = new Chart(ctx, {
            type: 'doughnut',
            data: chartData,
            options: {
                onClick: clickHandler,
                responsive: true,
                maintainAspectRatio: false
            }
        });
    });

    onDestroy(() => {
        if (chart) {
            chart.destroy();
        }
    });

    /** @param {any} evt */
    function clickHandler(evt) {
        const points = chart.getElementsAtEventForMode(evt, 'nearest', { intersect: false }, true);
      if (points.length) {
          const firstPoint = points[0];
          const label = chart.data.labels[firstPoint.index];
          const value = chart.data.datasets[firstPoint.datasetIndex].data[firstPoint.index];
          console.log(label, value);
      }

  }
</script>

<style>
    .chart {
        width: 400px;
        height: 400px;
        margin: 20px;
    }
</style>

<div class="chart">
    <canvas id={id}></canvas>
</div>
