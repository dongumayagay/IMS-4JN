<script>
    import { supabase } from "$lib/supabaseClient";
    import { goto } from "$app/navigation";
    let password;
    async function setPassword() {
        try {
            const { data, error } = await supabase.auth.update({ password });
            if (error) throw error;
            console.log(data);
            goto("/account");
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

<input bind:value={password} type="password" placeholder="password" />
<button on:click={setPassword}>set password</button>
