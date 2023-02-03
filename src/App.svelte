<script>
  import Todo from "./lib/Todo.svelte";
</script>

<div class="container">
  <h1>Creative <span>To-Do</span> List</h1>
  <div>
    <Todo />
  </div>
</div>

<style>
  h1 {
    font-size: 2.5rem;
    font-weight: 700;
    margin: 2rem 0;
    color: rgb(249, 253, 254);
  }
  span {
    color: rgb(41, 246, 250);
    text-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  }
</style>
