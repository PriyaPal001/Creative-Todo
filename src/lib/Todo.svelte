<script>
  let task = "";
  let todos = [];
  let filter = "all";
  function addTask() {
    todos = [{ task: task, status: "pending" }, ...todos];
    task = "";
  }

  function markcomplete(i) {
    todos[i].status = "completed";
    todos = [...todos];
  }

  function removeTask(i) {
    todos.splice(i, 1);
    todos = [...todos];}
</script>

<div class="container">
  <div class="todo">
    <div class="form">
      <input type="text" bind:value={task} />
      <button on:click={addTask}>ADD</button>
    </div>
{console.log(todos)}
    <div class="tasks">
      {#each todos as todo,i}
        {#if filter == "all"}
          <div class="task">
            <span class="color">{todo.task}</span>
            <button class="{todo.status=='completed'?'active':''}}"
              on:click={() => {
                markcomplete(i);
              }}>&#10004</button
            >
            <button
              on:click={() => {
                removeTask(i);
              }}>&#10006</button
            >
          </div>
        {:else if filter == "completed"}
          {#if todo.status == "completed"}
          <div class="task">
            <span class="color">{todo.task}</span>
            <button
              on:click={() => {
                removeTask(i);
              }}>&#10006</button
            >
          </div>
          {/if}
        {:else if filter == "incompleted"}
          {#if todo.status == "pending"}
          <div class="task">
            <span class="color">{todo.task}</span>
            <button class="{todo.status=='completed'?'active':''}}"
              on:click={() => {
                markcomplete(i);
              }}>&#10004</button
            >
          </div>
          {/if}
        {/if}
      {:else}{/each}
    </div>

    <div class="filters">
      <button
        class={filter == "all" ? "active" : ""}
        on:click={() => {
          filter = "all";
        }}>All</button
      >
      <button
        class={filter == "completed" ? "active" : ""}
        on:click={() => {
          filter = "completed";
        }}>Completed</button
      >
      <button
        class={filter == "incompleted" ? "active" : ""}
        on:click={() => {
          filter = "incompleted";
        }}>InCompleted</button
      >
    </div>
  </div>
</div>


<style>
  .color {
    color: red;
  }
</style>