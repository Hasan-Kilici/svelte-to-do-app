<script>
  import Icons from "./Icons.svelte";

  let newItem = "";
  let todoList = [];

  function addTodo() {
    if (newItem !== "") {
      todoList = [
        ...todoList,
        {
          task: newItem,
          completed: false,
        },
      ];
      newItem = "";
    }
  }

  function removeFromList(index) {
    todoList.splice(index, 1);
    todoList = todoList;
  }
</script>
<body>
<main class="container">
  <div>
    <form on:submit|preventDefault={addTodo}>
      <input
        bind:value={newItem}
        type="task"
        class="todos__input"
        placeholder="Görev ekle"
      />
      <button class="todos__button">+</button>
    </form>

    <h2 class="todos__listHeader">Yapılacak şeyler listesi</h2>

    {#each todoList as item, index}
      <div class="todo">
        <span
          class={`todo__text ${item.completed ? "todo__checked--strike" : ""}`}
          >{item.task}</span
        >

        <div class="icons">
          <button
            class="icon__button"
            on:click={() => (item.completed = !item.completed)}
          >
            <Icons name="check-mark" class="icon" />
          </button>

          <button class="icon__button" on:click={() => removeFromList(index)}>
            <Icons name="delete" class="icon" />
          </button>
        </div>
      </div>
    {/each}
  </div>
</main>
</body>
<style>
  body{
    margin:0;
    padding:0;
  }
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 90vh;
    padding-top: 10vh;
    margin:0;
    padding:0;
  }
  .todo {
    display: flex;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 10px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.2);
    -webkit-backdrop-filter: blur(25px);
    backdrop-filter: blur(25px);
    width: inherit;
    margin-top: 15px;
    font-size: 1.2rem;
    justify-content: space-between;
    align-items: center;
  }

  .todos__listHeader {
    text-align: center;
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 0 15px rgb(0 0 0 / 20%);
    background-color: hsla(0, 0%, 100%, 0.2);
    -webkit-backdrop-filter: blur(25px);
    backdrop-filter: blur(25px);
    margin: 15px 0px 25px 0px;
    font-size: 1.2rem;
  }

  .todos__input {
    background-color: inherit;
    border: none;
    box-shadow: none;
    text-decoration: none;
    font-size: 1.2rem;
    border:0.8px #eee solid;
    padding:8px;
    border-radius:8px;
    margin-top: 15px;
    outline: none;
    width: 500px;
  }

  .todos__button {
    background-color: inherit;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;
  }

  .icon__button {
    background-color: transparent;
    border: none;
    box-shadow: none;
    font-size: 1.2rem;
    cursor: pointer;
    color: rgba(0, 0, 0, 0.54);
  }
  .icon {
    background: rgba(0, 0, 0, 0.54);
  }

  .todo__checked--strike {
    text-decoration: line-through;
  }
</style>
