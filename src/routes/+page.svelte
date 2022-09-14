<script>
    import { user } from "$lib/stores";
    import Dashboard from "$lib/components/Dashboard.svelte";
    import Login from "$lib/components/Login.svelte";
    import Sidebar from "../lib/components/Sidebar.svelte";
</script>

{#if $user}
    <Dashboard />
{:else}
    <Sidebar/>
    <Login /> 
{/if}
