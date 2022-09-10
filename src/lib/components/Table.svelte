<script>
    import { supabase } from "../../lib/supabaseClient";
    import { onDestroy, onMount } from "svelte";

    let allItems = null;

    async function getAllItems() {
        try {
            let { data: items, error } = await supabase
                .from("items")
                .select("*");
            if (error) throw error;
            console.log(items);
            return items;
        } catch (error) {
            console.log(error);
        }
    }

    const itemsTableRealtimeListener = supabase
        .from("items")
        .on("*", async (payload) => {
            console.log("Items table changed", payload);
            allItems = await getAllItems();
        })
        .subscribe();

    onMount(async () => {
        allItems = await getAllItems();
    });
    onDestroy(() => {
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
                <button>add</button>
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
                    <button>update</button>
                </td>
            </tr>
        {:else}
            no items in the database
        {/each}
    </table>
{/if}

<style>
    td {
        border: 1px solid black;
        padding: 0.5rem;
    }
</style>
