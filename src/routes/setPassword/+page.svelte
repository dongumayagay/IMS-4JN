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

<div class="main">
    <div class="container">
        <h3>Set your Password</h3>
        <input bind:value={password} type="password" placeholder="Password" />
        <button on:click={setPassword}>Submit</button>
    </div>
    
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
    .container {
        width: 60vh;
        height: 27vw;
        background: #ffff;
    }
</style>
