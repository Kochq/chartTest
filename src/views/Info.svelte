<script lang="ts">
    import Equipo from "./../components/Equipo.svelte"
    export let params: any;

    let response = fetch(`http://localhost:8000/graficos/011/${params.id}`)
        .then(res => res.json())
        .then(data => data)
</script>

<main>
    <div class="container">
        {#await response}
            <div>Loading...</div>

            {:then response}
            {#each response as data}
                <Equipo {data}/>
            {/each}

            {:catch e}
            <p>Something went wrong {e}</p>
        {/await}
    </div>
</main>

<style>
.container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
</style>
