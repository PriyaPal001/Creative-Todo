<script>
  let task = "";
  let todos = JSON.parse(localStorage.getItem("1")) || [];
  let filter = "all";

  if (localStorage.length === 0) {
    localStorage.setItem("1", "[]");
  }

  function addTask() {
    todos = [{ task: task, status: "pending" }, ...todos];
    task = "";

    let mint = JSON.stringify(todos);
    localStorage.setItem("1", mint);
  }

  /**
   * @param {number} i
   */
  function markcomplete(i) {
    todos[i].status = "completed";
    todos = [...todos];
  }

  function removeTask(i) {
    todos.splice(i, 1);
    todos = [...todos];
  }
</script>

<div class="container">
  <div class="todo">
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
    <div class="form">
      <input type="text" bind:value={task} />
      <button on:click={addTask}>ADD</button>
    </div>
    <div class="tasks">
      {#each todos as todo, i}
        {#if filter == "all"}
          <div class="task">
            <span class="color">{todo.task}</span>
            <button
              class="{todo.status == 'completed' ? 'active' : ''}}"
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
              <button
                class="{todo.status == 'completed' ? 'active' : ''}}"
                on:click={() => {
                  markcomplete(i);
                }}>&#10004</button
              >
            </div>
          {/if}
        {/if}
      {/each}
    </div>
  </div>
</div>

<style>
  .color {
    font-size: 1.3rem;
    color: rgb(234, 233, 233);
    padding-right: 5px;
  }
  .filters {
    margin: 20px 0;
  }
  .filters button {
    margin: 0 3px;
    cursor: pointer;
  }
  .form {
    margin: 10px;
  }
  .form input {
    width: 250px;
    height: 40px;
    border: 2px solid rgb(62, 158, 255);
    border-radius: 5px;
    padding: 0 10px;
    font-family: sans-serif;
    margin: 0px 5px;
  }

  .task {
    width: fit-content;
    margin: 8px 0;
    border: 1px solid #ccc;
    padding: 10px 15px;
    border-radius: 3px;
    transition: all 0.3s ease;
  }
  .task:hover {
    transform: scale(1.04);
    background-color: rgba(204, 204, 204, 0.126);
    transition: all 0.3s ease;
    cursor: pointer;
    border-radius: 5px;
    border: 1px solid rgb(73, 182, 251);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
  }
  .tasks {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
  }
</style>
