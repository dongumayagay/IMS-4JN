<script>
    import { supabase } from "$lib/supabaseClient";
    import { goto } from "$app/navigation";
    let password;
    async function setPassword() {
        try {
            const { data, error } = await supabase.auth.update({ password });
            if (error) throw error;
            console.log(data);
            goto("/");
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

<div>
    <h3>set your password</h3>
    <input bind:value={password} type="password" placeholder="password" />
    <button on:click={setPassword}>set password</button>
</div>

<style>
    div {
        height: 100vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 0.5rem;
    }
</style>
