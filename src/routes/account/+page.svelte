<script>
    import { supabase } from "$lib/supabaseClient";
    import { goto } from "$app/navigation";

    async function logout() {
        try {
            const { error } = await supabase.auth.signOut();
            if (error) throw error;
            goto("/account/login");
        } catch (error) {
            console.log(error);
            alert("error occured");
        }
    }
</script>

<button on:click={logout}>logout</button>
