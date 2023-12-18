<!-- App.svelte -->
<script lang="ts">
    import Chart from './Chart.svelte';
    import { onMount } from 'svelte';

    interface ChartData {
        labels: string[];
        datasets: {
            label?: string;
            data?: number[];
            backgroundColor?: string[];
        }[];
    }

    let Reportando: ChartData = {
        labels: ['Reportando', 'No Reportando'],
        datasets: [{
            data: [],
            backgroundColor: ['green', 'red']
        }]
    };

    let Encendidos: ChartData = {
        labels: ['Encendidos', 'Apagados'],
        datasets: [{
            data: [],
            label: 'My Dataset 1',
            backgroundColor: ['green', 'red']
        }]
    };

    let Regando: ChartData = {
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
                Regando.datasets[0].data[0] = data.estaRegando.length;
                Regando.datasets[0].data[1] = data.noEstaRegando.length;
                Encendidos.datasets[0].data[0] = data.estaEncendido.length;
                Encendidos.datasets[0].data[1] = data.noEstaEncendido.length;
                Reportando.datasets[0].data[0] = data.estaReportando.length;
                Reportando.datasets[0].data[1] = data.noEstaReportando.length;
            })
            .catch(error => {
                Regando.datasets[0].data = [1,1];
                Encendidos.datasets[0].data = [1,1];
                Reportando.datasets[0].data = [1,1];
                console.error('Error fetching data:', error);
            });
    };

    onMount(() => {
        fetchDataAndUpdate('http://localhost:8000/graficos/011')

        setInterval(() => {
            fetchDataAndUpdate('http://localhost:8000/graficos/011')
        }, 5000);
    });
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
        <Chart chartData = {Reportando} id = {'chart1'} title = {"Equipos reportando"}/>
        <Chart chartData = {Encendidos} id = {'chart2'} title = {"Equipos encendidos"} />
        <Chart chartData = {Regando} id = {'chart3'} title = {"Equipos regando"} />
    </div>
</main>
