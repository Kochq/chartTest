<script lang="ts">
    import Chart from './../components/Chart.svelte';
    import { onMount, setContext } from 'svelte';

    let equipos = {
        estanRegando: {},
        noEstanRegando: {},
        estanEncendidos: {},
        noEstanEncendidos: {},
        estanReportando: {},
        noEstanReportando: {}
    };

    interface ChartData {
        labels: string[];
        datasets: {
            label?: string;
            data?: number[];
            backgroundColor?: string[];
        }[];
    }

    let estanReportando: ChartData = {
        labels: ['Reportando', 'No Reportando'],
        datasets: [{
            data: [],
            backgroundColor: ['green', 'red']
        }]
    };

    let estanEncendidos: ChartData = {
        labels: ['Encendidos', 'Apagados'],
        datasets: [{
            data: [],
            label: 'My Dataset 1',
            backgroundColor: ['green', 'red']
        }]
    };

    let estanRegando: ChartData = {
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
                equipos.estanRegando = data.estaRegando;
                equipos.noEstanRegando = data.noEstaRegando;
                equipos.estanEncendidos = data.estaEncendido;
                equipos.noEstanEncendidos = data.noEstaEncendido;
                equipos.estanReportando = data.estaReportando;
                equipos.noEstanReportando = data.noEstaReportando;

                estanRegando.datasets[0].data[0] = Object.keys(equipos.estanRegando).length;
                estanRegando.datasets[0].data[1] = Object.keys(equipos.noEstanRegando).length;
                estanRegando.datasets[0].label = 'estanRegando'
                estanEncendidos.datasets[0].data[0] = Object.keys(equipos.estanEncendidos).length;
                estanEncendidos.datasets[0].data[1] = Object.keys(equipos.noEstanEncendidos).length;
                estanEncendidos.datasets[0].label = 'estanEncendidos'
                estanReportando.datasets[0].data[0] = Object.keys(equipos.estanReportando).length;
                estanReportando.datasets[0].data[1] = Object.keys(equipos.noEstanReportando).length;
                estanReportando.datasets[0].label = 'estanReportando'
            })
            .catch(error => {
                estanRegando.datasets[0].data = [1,1];
                estanEncendidos.datasets[0].data = [1,1];
                estanReportando.datasets[0].data = [1,1];
                console.error('Error fetching data:', error);
            });
    };
    setContext('equipos', equipos);

    onMount(() => {
        fetchDataAndUpdate('http://localhost:8000/graficos2/011')

        setInterval(() => {
            fetchDataAndUpdate('http://localhost:8000/graficos2/011')
            console.log("fetch")
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
        <Chart chartData = {estanReportando} id = {'chart1'} title = {"Equipos reportando"}/>
        <Chart chartData = {estanEncendidos} id = {'chart2'} title = {"Equipos encendidos"} />
        <Chart chartData = {estanRegando} id = {'chart3'} title = {"Equipos regando"} />
    </div>
</main>
