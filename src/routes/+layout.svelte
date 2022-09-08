<script>
    import "../app.scss";
    import { supabase } from "$lib/supabaseClient.js";
    import { user } from "$lib/stores.js";
    import Navbar from "$lib/components/Navbar.svelte";

    user.set(supabase.auth.user());
    supabase.auth.onAuthStateChange((_, session) => {
        user.set(session?.user);
        console.log($user);
    });
</script>

<Navbar />
<slot />
