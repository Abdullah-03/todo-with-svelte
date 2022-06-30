<script>
    export let todos = []
  
    let totalTodos = todos.length
    let completedTodos = todos.filter(todos => todos.completed).length
  </script>
  
  <h1>Todo App</h1>
  
  <input type="text">
  <button>Add New Task</button>
  
  <h2>Remaining Tasks ({totalTodos - completedTodos})</h2>
  <ul>
    {#each todos.filter(todos => todos.completed == false) as todo, index(todo.id)}
      <li>
        <input type="checkbox" bind:checked={todo.completed}>
        {todo.name} (id: {todo.id})
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