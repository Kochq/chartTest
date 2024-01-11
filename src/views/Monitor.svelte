<script lang="ts">
    import Chart from './../components/Chart.svelte';
    import { onDestroy, onMount } from 'svelte';

    interface ChartData {
        labels: string[];
        datasets: {
            label?: string;
            data?: number[];
            backgroundColor?: string[];
        }[];
    }

    let intervalId: number;

    let reportando: ChartData = {
        labels: ['Reportando', 'No Reportando'],
        datasets: [{
            data: [],
            backgroundColor: ['green', 'red']
        }]
    };

    let encendidos: ChartData = {
        labels: ['Encendidos', 'Apagados'],
        datasets: [{
            data: [],
            label: 'My Dataset 1',
            backgroundColor: ['green', 'red']
        }]
    };

    let regando: ChartData = {
        labels: ['Regando', 'No Regando'],
        datasets: [{
            data: [],
            label: 'My Dataset 2',
            backgroundColor: ['green', 'red']
        }]
    };

    const fetchDataAndUpdate = (url: string) => {
        fetch(url)
            .then(response => response.json())
            .then(data => {
                regando.datasets[0].data[0] = data.estaRegando
                regando.datasets[0].data[1] = data.noEstaRegando
                regando.datasets[0].label = 'regando'
                encendidos.datasets[0].data[0] = data.estaEncendido
                encendidos.datasets[0].data[1] = data.noEstaEncendido
                encendidos.datasets[0].label = 'encendidos'
                reportando.datasets[0].data[0] = data.estaReportando
                reportando.datasets[0].data[1] = data.noEstaReportando
                reportando.datasets[0].label = 'reportando'
            })
            .catch(error => {
                regando.datasets[0].data = [1,1];
                encendidos.datasets[0].data = [1,1];
                reportando.datasets[0].data = [1,1];
                console.error('Error fetching data:', error);
            });
    };

    onMount(() => {
        fetchDataAndUpdate('http://localhost:8000/equipos/011/resumen')
        console.log("fetch monitor")

        intervalId = setInterval(() => {
            fetchDataAndUpdate('http://localhost:8000/equipos/011/resumen')
            console.log("fetch monitor")
        }, 5000);
    });

    onDestroy(() => clearInterval(intervalId)) // Stop the data fetching once the component is destroyed

</script>


<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    .allCharts {
        font-family: 'Roboto', sans-serif;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
    }
</style>

<main>
    <div class="allCharts">
        <Chart chartData = {reportando} id = {'chart1'} title = {"Equipos reportando"}/>
        <Chart chartData = {encendidos} id = {'chart2'} title = {"Equipos encendidos"} />
        <Chart chartData = {regando} id = {'chart3'} title = {"Equipos regando"} />
    </div>
</main>
