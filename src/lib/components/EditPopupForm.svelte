<script>
    import { scale } from "svelte/transition";
    import { supabase } from "../supabaseClient";
    export let selectedItem;
    $: showEditPopupForm = selectedItem !== null;

    async function submitHandler(event) {
        const formData = new FormData(event.target);
        const { name, description, unit, value } = Object.fromEntries(formData);
        const item = {
            name,
            description,
            unit,
            value,
            updatedAt: new Date().toISOString(),
        };
        console.log(selectedItem.updatedAt);
        console.log(new Date().toISOString().slice(0, -1));
        try {
            const { data, error } = await supabase
                .from("items")
                .update(item, { returning: "minimal" })
                .match({ id: selectedItem.id });
            if (error) throw error;
            console.log("updated", data);
            showEditPopupForm = false;
        } catch (error) {
            console.log(error);
            alert(error.message);
        }
    }
</script>

{#if showEditPopupForm}
    <main on:click|self={() => (showEditPopupForm = false)}>
        <form on:submit|preventDefault={submitHandler} transition:scale>
            <header>
                <h2>Edit Item</h2>
                <button
                    type="button"
                    on:click={() => (showEditPopupForm = false)}
                    id="close">x</button
                >
            </header>
            <input
                required
                name="name"
                type="text"
                placeholder="Item name"
                value={selectedItem.name}
            />
            <input
                name="description"
                type="text"
                placeholder="Item description"
                value={selectedItem.description}
            />
            <input
                name="unit"
                required
                type="text"
                placeholder="unit of measurement (grams/kg/meter/liter)"
                value={selectedItem.unit}
            />
            <input
                name="value"
                required
                type="number"
                placeholder="value"
                min="1"
                value={selectedItem.value}
            />
            <button type="submit">Edit item</button>
        </form>
    </main>
{/if}

<style>
    main {
        background-color: rgba(0, 0, 0, 0.5);
        position: fixed;
        top: 0px;
        right: 0px;
        bottom: 0px;
        left: 0px;
        display: grid;
        place-items: center;
        padding: 1rem;
    }
    form {
        background-color: white;
        padding: 1rem;
        width: 100%;
        max-width: 512px;
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
    }
    header {
        position: relative;
    }
    h2 {
        text-align: center;
    }
    #close {
        position: absolute;
        right: 0;
        top: 0;
        border: none;
        background-color: red;
        aspect-ratio: 1/1;
    }
    input {
        border: 1px solid black;
        padding: 0.25rem;
        width: 100%;
    }
    button[type="submit"] {
        width: 100%;
        padding: 0.25rem;
    }
</style>
