<script>
    import { fade } from "svelte/transition";
</script>

<main out:fade={{ duration: 10}}>
    <img src="/images/logo.jpg" alt="4JN Metal Fabrication Company">
    <h1>4JN Metal Fabrication Company</h1>
    <h2>Inventory Management System</h2>
</main>

<style>
    main {
        height: 100vh;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: #0A1A4E;
    }
    img {
        margin-top: 200px;
        object-fit: fill;
    }
</style>
