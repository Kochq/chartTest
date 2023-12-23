<script>
    import { getContext } from "svelte";

    export let params;
    const { id } = params;

    let esto = getContext('equipos');
    console.log(esto)
</script>

<main>
    <p>{id}</p>
</main>
