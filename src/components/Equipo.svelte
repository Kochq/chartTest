<script>
    export let data
    const {day, direccion2, direction, horimetro, id, lat, lng, porcentajeAvance, presion, regando, rumbo, stat, tension, time} = data
    let backgroundColor = stat ? 'green' : 'red';
</script>


<main>
    <div class="container" style="background-color: {backgroundColor};">
        <p>{id}</p>
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
}
</style>
