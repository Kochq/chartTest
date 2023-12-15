<script>
    import { onMount, onDestroy, afterUpdate, setContext } from 'svelte';
    import Chart from 'chart.js/auto';

    export let chartData;
    export let title = "Chart"
    export let id;

    let chart;  

    function initializeChart() {
        const ctx = document.getElementById(id);

        // @ts-ignore
        chart = new Chart(ctx, {
            type: 'doughnut',
            data: chartData,
            options: {
                onClick: clickHandler,
                maintainAspectRatio: false
            }
        });
    }    

    onMount(() => {
        initializeChart();
    });

    afterUpdate(() => {
        chart.data = chartData;
        chart.update();
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
    h1 {
        font-size: 1.5rem;
    }
    .chart {
        display: flex;
        align-items: center;
        flex-direction: column;
        width: 400px;
        height: 250px;
        margin: 20px;
    }
</style>
<div class="chart">
    <h1>{title}</h1>
    <canvas id={id}></canvas>
</div>
