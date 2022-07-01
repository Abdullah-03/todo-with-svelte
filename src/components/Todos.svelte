  <script>
    import Todo from './Todo.svelte'

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

    function updateTodo(todo) {
      const i = todos.findIndex(t => t.id === todo.id)
      todos[i] = { ...todos[i], ...todo }
    }


    function editTodo(todo){
      let newName = prompt('new name: ')
      todo.name = newName

      deleteTodo(todo)
      todos.push(todo)

      todos=todos
    }

    // let filter = 'all'
    // const filterTodos = (filter, todos) =>
    //   filter === 'active' ? todos.filter(t => !t.completed) :
    //   filter === 'completed' ? todos.filter(t => t.completed) :
    //   todos

  </script>
  
  <main>
    
  
  <h1>Todo App</h1>
  
  <div class="add-todo">
    <form on:submit|preventDefault={addTodo}>
      <label for="newTodo">😎 Get work done!</label>
      <input type="text" bind:value={newTodoName}>
      <button type="submit">Add</button>
    </form>
  </div>

  <!-- <button on:click={() => filter = 'all'}>Show all Tasks</button>
  <button on:click={() => filter = 'completed'}>Show Completed Tasks</button>
  <button on:click={() => filter = 'remaining'}>Show Remaining Tasks</button> -->
  
  <h3>Remaining Tasks ({totalTodos - completedTodos})</h3>
  <ul>
    {#each todos.filter(todos => todos.completed == false) as todo, index(todo.id)}
      <li>
        <Todo {todo}
          on:remove={e => deleteTodo(e.detail)}
          on:update={e => updateTodo(e.detail)}
        />
      </li>
  
    {:else}
      <li>
        <p>🥳 Congrats! You're all caught up</p>
      </li>
    {/each}
  </ul>
  
  <h3>Completed Tasks ({completedTodos})</h3>
  <ul>
    {#each todos.filter(todos => todos.completed == true) as todo, index(todo.id)}
      <li>
        <Todo {todo}
          on:remove={e => deleteTodo(e.detail)}
          on:update={e => updateTodo(e.detail)}
        />
      </li>
  
    {:else}
      <li>
        <p>💪 Time to get started on those tasks</p>
      </li>
    {/each}
  </ul>
  
</main>

  <style>
    *{
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }
  
    p{
      color: #EEEEEE;
    }

    h1{
      text-align: center;
      color: #EEEEEE;
    }

    h3{
      text-align: left;
      color: #EEEEEE;
    }

    li{
      list-style-type: none;
    }

    label{
      color: blanchedalmond;
    }

    main{
      height:100%;
      background-color: #222831;
    }

    .add-todo{
      padding-left: 30%;
    }

  </style>