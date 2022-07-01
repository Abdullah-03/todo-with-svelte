<script>
  import Todos from './components/Todos.svelte'

  let todos = [
    { id: 1, name: 'Create a Svelte starter app', completed: true },
    { id: 2, name: 'Create your first component', completed: true },
    { id: 3, name: 'Complete the rest of the tutorial', completed: false }
  ]
</script>

<main>
  <Todos todos={todos} />
</main>


<style>
  :global(body) {
		/* this will apply to <body> */
		margin: 0;
    height: 100%;
	}

  :global(html){
    height: 100%;
  }

  :global(#app){
    height: 100%;
  }

  main{
    height: 100%;
  }
</style>
