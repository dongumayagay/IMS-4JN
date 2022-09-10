<script>
    // import { supabase } from "$lib/supabaseClient";
    import { user } from "$lib/stores";
    import { supabase } from "../../lib/supabaseClient";
    import Table from "./Table.svelte";

    async function logout() {
        try {
            const { error } = await supabase.auth.signOut();
            if (error) throw error;
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

<h1>Dashboard</h1>
<main>
    <h4>{$user.email}</h4>
    <button on:click={logout}>logout</button>
</main>
<Table />

<style>
    main {
        display: flex;
        align-items: center;
        gap: 1rem;
    }
</style>
