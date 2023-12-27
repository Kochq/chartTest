<script>
    export let data
    const {
        lat,
        lng,
        day,
        stat,
        time,
        rumbo,
        regando,
        tension,
        presion,
        nombreEq,
        direction,
        horimetro,
        direccion2,
        porcentajeAvance,
    } = data

    let backgroundColor = stat ? 'green' : 'red';

</script>


<main>
    <div class="container" style="background-color: {backgroundColor};">
        <p>{nombreEq}</p>
        <p>Ultimo reporte {day} {time}</p>
        {#if stat}
           <p>Esta encendido</p> 
        {:else}
            <p>No esta encendido</p>
        {/if}
    </div>
</main>


<style>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 1px solid black;
    margin: 5px;
    padding: 10px;
    border-radius: 5px;
}
</style>
