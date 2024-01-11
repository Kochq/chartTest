<script>
    export let data
    const {
        lat,
        lng,
        dia,
        stat,
        hora,
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

<div class="container" style="background-color: {backgroundColor};">
    <p>{nombreEq}</p>
    <p>Ultimo reporte {dia} {hora}</p>
    {#if stat}
        <p>Esta encendido</p>
    {:else}
        <p>No esta encendido</p>
    {/if}
</div>

<style>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 5px;
    padding: 10px;
    border-radius: 5px;
}
</style>
