<script>
    import { supabase } from "$lib/supabaseClient";

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

<button on:click={logout}>logout</button>
