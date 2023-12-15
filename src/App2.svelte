<!-- App.svelte -->
<script>
    import Chart from './Chart.svelte';
    import { onMount } from 'svelte';


    let Reportando = {
        labels: ['Reportando', 'No Reportando'],
        datasets: [{
            backgroundColor: ['green', 'red']
        }]
    };

    let Encendidos = {
        labels: ['Encendidos', 'Apagados'],
        datasets: [{
            label: 'My Dataset 1',
            backgroundColor: ['green', 'red']
        }]
    };

    let Regando = {
        labels: ['Regando', 'No Regando'],
        datasets: [{
            data: [0, 0],
            label: 'My Dataset 2',
            backgroundColor: ['green', 'red']
        }]
    };

    onMount(() => {
        fetch('http://localhost:8000/graficos/011')
            .then(response => response.json())
            .then(data => {
                Regando.datasets[0].data[1] = data.estaRegando.length;
                Regando.datasets[0].data[0] = data.noEstaRegando.length;
                Encendidos.datasets[0].data[1] = data.estaEncendido.length;
                Encendidos.datasets[0].data[0] = data.noEstaEncendido.length;
                Reportando.datasets[0].data[1] = data.estaReportando.length;
                Reportando.datasets[0].data[0] = data.noEstaReportando.length;
            })
            .catch(error => {
                Regando.datasets[0].data = [1,1];
                Encendidos.datasets[0].data = [1,1];
                Reportando.datasets[0].data = [1,1];
                console.error('Error fetching data:', error);
            });
    });
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
        <Chart chartData = {Reportando} id = {'chart1'} title = {"Equipos reportando"}/>
        <Chart chartData = {Encendidos} id = {'chart2'} title = {"Equipos encendidos"} />
        <Chart chartData = {Regando} id = {'chart3'} title = {"Equipos regando"} />
    </div>
</main>
