<script>
    import { user } from "$lib/stores";

    $: link = $user ? "/account" : "/account/login";
</script>

<h1>Welcome to 4JN Metal Fabrication Inventory Management System</h1>

<a href={link}> Go to Account </a>
