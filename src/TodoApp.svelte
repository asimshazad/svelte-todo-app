<script>
  let newTodo = '';
  let todos = [
    { text: 'Debug the debugger', completed: false },
    { text: 'Break reminder function', completed: false },
    { text: 'Placeholder for brilliance', completed: true },
  ];

  function addTodo() {
    if (newTodo.trim()) {
      todos = [...todos, { text: newTodo, completed: false }];
      newTodo = '';
    }
  }

  function toggleTodo(index) {
    todos = todos.map((todo, i) =>
      i === index ? { ...todo, completed: !todo.completed } : todo
    );
  }

  function deleteTodo(index) {
    todos = todos.filter((_, i) => i !== index);
  }
</script>

<div class="max-w-lg mx-auto mt-10 p-6 bg-white shadow-md rounded-lg">
  <h1 class="text-2xl font-bold text-center mb-6">Svelte TODO App</h1>
  
  <div class="mb-4">
    <input
      type="text"
      class="border w-full px-3 py-2 rounded-md focus:outline-none"
      bind:value={newTodo}
      placeholder="Add new todo"
    />
    <button
      class="mt-2 w-full bg-blue-500 text-white px-4 py-2 rounded-md hover:bg-blue-600"
      on:click={addTodo}
    >
      Add TODO
    </button>
  </div>

  <ul>
    {#each todos as todo, index}
      <li class="flex justify-between items-center p-2 bg-gray-100 mb-2 rounded-md">
        <span
          class:line-through={todo.completed}
          class="cursor-pointer"
          on:click={() => toggleTodo(index)}
        >
          {todo.text}
        </span>
        <button
          class="bg-red-500 text-white px-2 py-1 rounded-md hover:bg-red-600"
          on:click={() => deleteTodo(index)}
        >
          Delete
        </button>
      </li>
    {/each}
  </ul>
</div>

<style>
  .line-through {
    text-decoration: line-through;
  }
</style>
