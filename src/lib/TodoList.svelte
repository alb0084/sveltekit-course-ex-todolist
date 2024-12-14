<svelte:options immutable={true} />

<script>
    import { v4 as uuid } from "uuid";
    import { createEventDispatcher } from "svelte";

    export let todos = [];
    let inputText = "";
    const dispatch = createEventDispatcher();

    function handleAddTodo() {
        const isNotCancelled = dispatch(
            "addtodo",
            {
                title: inputText,
            },
            { cancelable: true },
        );
        if (isNotCancelled) {
            inputText = "";
        }
    }

    function handleRemoveEvent(id) {
        dispatch("removetodo", {
            id,
        });
        console.log("Remove button clicked");
    }

    function hendleToggleEvent(id, value) {
        dispatch("toggletodo", {
            id,
            value,
        });
        console.log("Toggle button clicked");
    }
</script>

<div>
    <ul>
        {#each todos as { id, title, completed } (id)}
            <li>
                <label>
                    <input
                        on:input={(event) => {
                            event.currentTarget.checked = completed;
                            hendleToggleEvent(id, !completed);
                        }}
                        type="checkbox"
                        checked={completed}
                    />
                    {completed}
                    {title}
                </label>
                <button on:click={() => handleRemoveEvent(id)}>Remove</button>
            </li>
        {/each}
    </ul>
    {inputText}
    <form class="add-todo-form" on:submit|preventDefault={handleAddTodo}>
        <input bind:value={inputText} />
        <button type="submit" disabled={!inputText}>Add</button>
    </form>
</div>

<style>
</style>
