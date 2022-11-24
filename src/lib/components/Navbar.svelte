<script>
      import { user } from "$lib/stores";
      import { supabase } from "../supabaseClient";
      import Table from "../compo/Table.svelte";
  
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

<main>
      <h1>Dashboard</h1>
      <div>
          <h4>{$user.email}</h4>
          <button class="btn btn-danger" on:click={logout}>logout</button>
      </div>
      <Table />
      
</main>