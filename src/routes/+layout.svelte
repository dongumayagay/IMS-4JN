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
        <div in:fade>
            <slot />
        </div>
    {/if}
</main>

<style>
    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }
    main {
        font-family: "Poppins", sans-serif; 
        background : #0A1A4E;
        overflow: hidden;
        height: 100vh;
    }
</style>
