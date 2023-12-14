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
      data: [15, 25, 35],
      backgroundColor: ['purple', 'black', 'brown']
    }]
  };

</script>

<main>
    <div style="display: flex; flex-wrap: wrap; justify-content: center;">
        <Chart chartData = {chartData1} id = {'chart1'} />
    </div>
</main>
