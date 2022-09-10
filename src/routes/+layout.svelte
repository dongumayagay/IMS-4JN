<script>
    import "../app.scss";
    import { supabase } from "$lib/supabaseClient.js";
    import { user } from "$lib/stores.js";
    import { onMount } from "svelte";

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

{#if show === false}
    <main>
        <section>
            <h1>4JN Metal Fabrication Company</h1>
            <h2>Inventory Management System</h2>
        </section>
    </main>
{:else}
    <slot />
{/if}

<style>
    main {
        height: 100vh;
        display: grid;
        place-items: center;
    }
    section {
        text-align: center;
    }
</style>
