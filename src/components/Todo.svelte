<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()

    export let todo

    let editing = false                     // track editing mode
    let name = todo.name 


    function update(updatedTodo) {
        todo = { ...todo, ...updatedTodo }    // applies modifications to todo
        dispatch('update', todo)              // emit update event
    }

    function onCancel() {
        name = todo.name                      // restores name to its initial value and
        editing = false                       // and exit editing mode
    }

    function onSave() {
        update({ name: name })                // updates todo name
        editing = false                       // and exit editing mode
    }

    function onRemove() {
        dispatch('remove', todo)              // emit remove event
    }

    function onEdit() {
        editing = true                        // enter editing mode
    }

    function onToggle() {
        update({ completed: !todo.completed}) // updates todo status
    }

</script>

 {#if editing}

 <label for="update-name">New name for task: </label>
 <input type="text" bind:value={name} id="update-name">
 <button on:click={onSave} disabled={!name}>Save</button>
 <button on:click={onCancel} class="danger-btn">Cancel</button>

 {:else}

 <input type="checkbox" checked={todo.completed} on:click={onToggle}>
 <span>{todo.name}</span>
 <button on:click={onRemove} class="danger-btn">Delete</button>
 <button on:click={onEdit}>Edit</button>

 {/if}

 <style>
    button{
        background-color: #00ADB5;
        border: 5px solid #00ADB5;
        border-radius: 5px;
    }

    .danger-btn{
        background-color: #E84545;
        border: 5px solid #E84545;
        border-radius: 5px;
    }

    span{
        color: #EEEEEE  ;
    }
 </style>