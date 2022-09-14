<script>
    import { user } from "$lib/stores";
    import { supabase } from "../../lib/supabaseClient";
    import Sidebar from "./Sidebar.svelte";
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

<Sidebar/>
<main>
    <h1>Dashboard</h1>
    <div>
        <h4>{$user.email}</h4>
        <button class="btn btn-danger" on:click={logout}>logout</button>
    </div>
    <Table />
</main>

<style>
    h1 {
        color: blue;
    }
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;
    }
    div {
        display: flex;
        gap: 1rem;
    }
</style>
