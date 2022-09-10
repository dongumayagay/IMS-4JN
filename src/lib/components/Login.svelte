<script>
    import { supabase } from "$lib/supabaseClient";

    let email, password;

    async function login() {
        try {
            const { data, error } = await supabase.auth.signIn({
                email,
                password,
            });
            if (error) throw error;
            console.log("login success\nuser info", data);
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

<h1>Login</h1>
<p>if you don't have access yet please contact admin</p>
<form on:submit|preventDefault={login}>
    <input bind:value={email} type="email" placeholder="Email" />
    <input bind:value={password} type="password" placeholder="password" />
    <button>Login</button>
</form>
