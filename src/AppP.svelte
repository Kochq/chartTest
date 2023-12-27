<!-- App.svelte -->
<script>
    import Chart from './Chart.svelte';

    const chartData1 = {
        labels: ['Fallas', 'Funcionando', 'Warning'],
        datasets: [{
            data: [345,231,23],
            backgroundColor: ['Red', 'Green', 'Yellow']
        }]
    };

    const chartData2 = {
        labels: ['Label 1', 'Label 2', 'Label 3'],
        datasets: [{
            label: 'My Dataset 1',
            data: [10, 20, 30],
            backgroundColor: ['red', 'green', 'blue']
        }]
    };

    const chartData3 = {
       labels: ['Label A', 'Label B', 'Label C'],
        datasets: [{
            label: 'My Dataset 2',
            data: [57, 124, 100],
            backgroundColor: ['purple', 'black', 'brown']
        }]
    };

</script>

<style>
    .allCharts {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
</style>

<main>
    <div class="allCharts">
        <Chart chartData = {chartData1} id = {'chart1'} title = {"Equipos reportando"}/>
        <Chart chartData = {chartData2} id = {'chart2'} title = {"Equipos encendidos"} />
        <Chart chartData = {chartData3} id = {'chart3'} title = {"Equipos regando"} />
    </div>
</main>
