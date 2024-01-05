<!-- App.svelte -->
<script lang="ts">
    import router from 'page'
    import Monitor from './views/Monitor.svelte'
    import Info from './views/Info.svelte';
    import Home from './components/Home.svelte';

    let page: any

    let params:any
    router('/', () => page = Home)
    router('/info/:id', (ctx: any,next: any) => { params = ctx.params; next(); }, () => page = Info)
    router('/monitor', () => page = Monitor)

    router.start()
</script>

{#if params != null}
    <svelte:component this={page} {params} />
{:else}
    <svelte:component this={page} />
{/if}


<style>
</style>

<main>
</main>
