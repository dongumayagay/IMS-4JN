<script>
    import "../app.scss";
    import { supabase } from "$lib/supabaseClient.js";
    import { user } from "$lib/stores.js";
    import { onMount } from "svelte";
    import { fade } from "svelte/transition";
    import Loading from "../lib/components/Loading.svelte";
    $user = supabase.auth.user();
    supabase.auth.onAuthStateChange((_, session) => {
        $user = session ? session?.user : null;
    });

    let show = false;

    onMount(() => {
        show = true;
    });
</script>

<svelte:head>
    <title>4JN IMS</title>
</svelte:head>

<main>
    {#if show === false}
        <Loading />
    {:else}
        <div in:fade={{ delay: 400 }}>
            <slot />
        </div>
    {/if}
</main>

<style>
    main {
        overflow: hidden;
        height: 100vh;
    }
</style>
