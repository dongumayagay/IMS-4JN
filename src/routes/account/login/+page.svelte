<script>
    import { supabase } from "$lib/supabaseClient";
    import { goto } from "$app/navigation";

    let email, password;

    async function login() {
        try {
            const { data, error } = await supabase.auth.signIn({
                email,
                password,
            });
            if (error) throw error;
            console.log(data);
            goto("/account");
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

<input bind:value={email} type="email" placeholder="Email" />
<input bind:value={password} type="password" placeholder="password" />
<button on:click={login}>Login</button>
