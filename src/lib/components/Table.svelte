<script>
    import { supabase } from "../../lib/supabaseClient";
    import { onDestroy, onMount } from "svelte";
    import AddPopupForm from "./AddPopupForm.svelte";
    import EditPopupForm from "./EditPopupForm.svelte";

    let allItems = null;
    let showAddPopupForm = false;
    let selectedItem = null;

    // function to get all items from the database
    async function getAllItems() {
        try {
            let { data: items, error } = await supabase
                .from("items")
                .select("*");
            if (error) throw error;
            return items;
        } catch (error) {
            console.log(error);
        }
    }

    // listen to changes to items table
    const itemsTableRealtimeListener = supabase
        .from("items")
        .on("*", async (payload) => {
            console.log("Items table changed", payload);
            // if there is a new item update UI to add the new Item as well
            if (payload.eventType === "INSERT")
                allItems = [...allItems, payload.new];
            // if an item is updated. find the corresponding item in the list and change the value to reflect the changes as well
            if (payload.eventType === "UPDATE") {
                const id = payload.old.id;
                const itemIndex = allItems.findIndex((item) => item.id == id);
                allItems[itemIndex] = payload.new;
                allItems = [...allItems];
            }
            // if item is deleted on the databse, delete that item on the UI as well
            if (payload.eventType === "DELETE")
                allItems = allItems.filter((item) => item.id != payload.old.id);
        })
        .subscribe();

    onMount(async () => {
        // on mounting of this component call the getAllItem to get all the items from the databse
        allItems = await getAllItems();
    });
    onDestroy(() => {
        // on destrooy of this component unsuscribe to realtime changes for both client and server cost effiiciency
        itemsTableRealtimeListener.unsubscribe();
    });
</script>

{#if allItems === null}
    loading
{:else}
    <table>
        <tr>
            <td>name</td>
            <td>description</td>
            <td>value</td>
            <td>unit</td>
            <td>last updated</td>
            <td>
                <button
                    class="btn btn-success"
                    on:click={() => {
                        showAddPopupForm = true;
                    }}>Add</button
                >
            </td>
        </tr>
        {#each allItems as item}
            <tr>
                <td>
                    {item.name}
                </td>
                <td>
                    {item.description}
                </td>
                <td>
                    {item.value}
                </td>
                <td>
                    {item.unit}
                </td>
                <td>
                    {new Intl.DateTimeFormat("en-PH", {
                        dateStyle: "full",
                        timeStyle: "long",
                    }).format(new Date(item.updatedAt))}
                </td>
                <td>
                    <button
                        class="btn btn-info"
                        on:click={() => {
                            selectedItem = item;
                        }}>Edit</button
                    >
                </td>
            </tr>
        {:else}
            no items in the database
        {/each}
    </table>
{/if}

<AddPopupForm bind:showAddPopupForm />
<EditPopupForm bind:selectedItem />

<style>
    td {
        border: 1px solid black;
        padding: 0.5rem;
    }
</style>
