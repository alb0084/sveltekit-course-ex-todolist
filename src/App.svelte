<script>
  import TodoList from "./lib/TodoList.svelte";
  import { v4 as uuid } from "uuid";
  let todos = [
    { id: uuid(), title: "Todo 1", completed: true },
    { id: uuid(), title: "Todo 2", completed: true },
    { id: uuid(), title: "Todo 1", completed: true },
  ];
  function handleAddTodo(event) {
    // event.preventDefault();
    todos = [
      ...todos,
      { id: uuid(), title: event.detail.title, completed: false },
    ];
  }
  function handleRemoveTodo(event) {
    todos = todos.filter((t) => t.id !== event.detail.id);
  }
  function handleToggleTodo(event) {
    todos = todos.map((todo) => {
      if (todo.id === event.detail.id) {
        return { ...todo, completed: event.detail.value };
      }
      return { ...todo };
    });
  }
</script>

<TodoList
  {todos}
  on:toggletodo={handleToggleTodo}
  on:removetodo={handleRemoveTodo}
  on:addtodo={handleAddTodo}
/>

<style>
</style>
