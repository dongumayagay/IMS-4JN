<script>
    import { supabase } from "$lib/supabaseClient";
    import { user } from "$lib/stores";
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
<p>{$user.email}</p>
<button on:click={logout}>logout</button>
