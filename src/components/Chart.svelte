<script>
    import { onMount, onDestroy, getContext, setContext } from 'svelte';
    import router from 'page';
    import Chart from 'chart.js/auto';

    export let chartData;
    export let title = "Chart"
    export let id;

    let esto = getContext('equipos');
    setContext('equipo', esto)

    console.log(esto)

    let chart;  

    onMount(() => {
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
    });

    onDestroy(() => {
        if (chart) {
            chart.destroy();
        }
    });

    $: if(chart) {
        chart.data = chartData;
        chart.update();
    }

    /** @param {any} evt */
    function clickHandler(evt) {
        const points = chart.getElementsAtEventForMode(evt, 'nearest', { intersect: true }, true);
        if (points.length) {
            const firstPoint = points[0];
            const label = chart.data.labels[firstPoint.index];
            const esto = chart.data.datasets[0].label
            const value = chart.data.datasets[firstPoint.datasetIndex].data[firstPoint.index];
            console.log(label + ":" , value);
            router('/info/' + esto, { replace: true }, { id: label })
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
    {#if chartData.datasets[0].data < 1}
        <div>Loading...</div>
    {/if}
    <canvas id={id}></canvas>
    {#if chartData.datasets[0].data.length > 0}
        <br>
        <div>{chartData.labels[0]}: {chartData.datasets[0].data[0]}</div>
        <div>{chartData.labels[1]}: {chartData.datasets[0].data[1]}</div>
    {/if}
</div>
