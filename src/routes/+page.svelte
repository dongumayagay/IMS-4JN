<script>
    import { user } from "$lib/stores";
    import Dashboard from "../lib/components/Dashboard.svelte";
    import Login from "../lib/components/Login.svelte";
</script>

<h1>Welcome to 4JN Metal Fabrication Inventory Management System</h1>

{#if $user}
    <Dashboard />
{:else}
    <Login />
{/if}
