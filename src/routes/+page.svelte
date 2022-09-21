<script>
    import { user } from "$lib/stores";
    import Dashboard from "$lib/components/Dashboard.svelte";
    import Inventory from "$lib/components/Inventory.svelte";
    import Login from "$lib/components/Login.svelte";

    let page = "dashboard";
</script>

{#if $user}
    <nav>
        <button on:click={() => (page = "dashboard")}>dashboard</button>
        <button on:click={() => (page = "inventory")}>inventory</button>
    </nav>

    {#if page === "dashboard"}
        <Dashboard />
    {:else if page === "inventory"}
        <Inventory />
    {/if}
{:else}
    <Login />
{/if}
