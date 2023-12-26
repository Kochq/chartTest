<script lang="ts">
    import { onMount } from "svelte";
    import Equipo from "./Equipo.svelte"


    export let params;
    const { id } = params;
    let response;


    response = fetch(`http://localhost:8000/graficos/011/${id}`)
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
}
</style>
