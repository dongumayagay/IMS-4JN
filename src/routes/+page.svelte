<script>
    import { user } from "$lib/stores";
    import Dashboard from "$lib/components/Dashboard.svelte";
    import Login from "$lib/components/Login.svelte";
</script>

{#if $user}
    <Dashboard />
{:else}
    <Login />
{/if}
