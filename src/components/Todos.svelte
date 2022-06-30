  <script>
    export let todos = []
  
    $: totalTodos = todos.length
    $: completedTodos = todos.filter(todos => todos.completed).length
    let newTodoName = ''
    let newTodoId
      $:{
        if (todos.length == 0) {
          newTodoId = 1
        }
        else{
          newTodoId = todos[todos.length - 1].id + 1;
        }
      }

    function addTodo() {
      todos.push({ id: newTodoId, name: newTodoName, completed: false })
      newTodoName = ''
      todos=todos
    }


    function deleteTodo (todo){
      todos = todos.filter(t => t.id != todo.id)
    }

    // let filter = 'all'
    // const filterTodos = (filter, todos) =>
    //   filter === 'active' ? todos.filter(t => !t.completed) :
    //   filter === 'completed' ? todos.filter(t => t.completed) :
    //   todos

  </script>
  
  <h1>Todo App</h1>
  
  <form on:submit|preventDefault={addTodo}>
    <label for="newTodo">😎 Get work done!</label>
    <input type="text" bind:value={newTodoName}>
    <button type="submit">Add</button>
  </form>
  
  <!-- <button on:click={() => filter = 'all'}>Show all Tasks</button>
  <button on:click={() => filter = 'completed'}>Show Completed Tasks</button>
  <button on:click={() => filter = 'remaining'}>Show Remaining Tasks</button> -->
  
  <h2>Remaining Tasks ({totalTodos - completedTodos})</h2>
  <ul>
    {#each todos.filter(todos => todos.completed == false) as todo, index(todo.id)}
      <li>
        <input type="checkbox" bind:checked={todo.completed}>
        {todo.name} (id: {todo.id})
        <button on:click={() => deleteTodo(todo)}>Delete</button>
      </li>
  
    {:else}
      <li>
        <p>🥳 Congrats! You're all caught up</p>
      </li>
    {/each}
  </ul>
  
  <h2>Completed Tasks ({completedTodos})</h2>
  <ul>
    {#each todos.filter(todos => todos.completed == true) as todo, index(todo.id)}
      <li>
        <input type="checkbox" bind:checked={todo.completed}>
        {todo.name} (id: {todo.id})
        <button on:click={() => deleteTodo(todo)}>Delete</button>
      </li>
  
    {:else}
      <li>
        <p>💪 Time to get started on those tasks</p>
      </li>
    {/each}
  </ul>
  
  
  <style>
    *{
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
  
    li{
      list-style-type: none;
    }
  
    .rem-task-text{
      display: inline-block;
    }
  
    .com-task-text{
      display: inline-block;
      text-decoration: line-through;
    }
    
  </style>