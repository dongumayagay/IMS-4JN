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

{#if show === false}
    loading
{:else}
    <slot />
{/if}
