<template>
  <div id="app" class="container">
    <h1>Todo-list</h1>
    <div class="header-input">
      <input
        type="text"
        class="todo-input"
        placeholder="Write a new task"
        v-model="newTodo"
        @keyup.enter="addTodo"
      />
      <button @click="addTodo" class="todo-button">
        <i class="fas fa-plus-square"></i>
      </button>
    </div>
    <div v-if="isEmpty" class="empty">List is empty please add something</div>
    <div v-else class="todo-list">
      <ul>
        <li
          v-for="(todo, index) in todos"
          :key="todo.title"
          class="todo-item"
          :class="{ completed: todo.completed }"
        >
          {{ todo.title }}
          <input
            type="checkbox"
            v-model="todo.completed"
            class="complete-btn"
          />
          <button @click="removeTodo" class="trash-btn">
            <i class="fas fa-trash"></i>
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-list",
  data() {
    return {
      newTodo: "",
      todos: [],
    };
  },
  computed: {
    isEmpty: function () {
      if (this.todos.length == 0) {
        return true;
      }
    },
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length == 0) {
        alert("Please type something");
        return;
      }
      this.todos.push({
        title: this.newTodo,
        completed: false,
      });
      this.newTodo = "";
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  font-family: "Abel", sans-serif;
  background: rgb(241, 241, 241);
  color: black;
  min-height: 88vh;
  transition: all 0.5s ease;
}
input {
  padding: 1rem;
  font-size: 1.5rem;
  border: none;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}
.container {
  max-width: 720px;
  margin: 0 auto;
}
.logo {
  display: block;
  margin: 20px auto;
  height: 75px;
}
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  background: linear-gradient(124.11deg, #057c52 3.52%, #00ae72 41.89%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
  text-transform: uppercase;
  font-family: "Montserrat", sans-serif;
}
.header-input {
  display: flex;
  border-radius: 18px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 5rem;
}
header,
input,
button {
  padding: 1rem;
  font-size: 1.5rem;
  border: none;
  font-family: "Abel", sans-serif;
}
input {
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}
input:focus {
  outline: none;
}
button {
  color: rgb(65, 65, 65);
  background: white;
  cursor: pointer;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
  transition: all 0.5s ease;
  outline: none;
}
button:hover {
  color: #2ca54a;
}
.todo-list {
  margin-top: 3rem;
}
.todo-item {
  background: white;
  padding: 0rem 0.5rem;
  margin: 1rem;
  height: 60px;
  color: black;
  font-size: 1.5rem;
  display: flex;
  align-items: center;
  transition: all 0.5s ease;
  border-radius: 8px;
}
.complete-btn {
  margin-left: auto;
  background: none;
}
.trash-btn {
  background: none;
}
.trash-btn:hover {
  color: rgb(212, 68, 68);
}
.completed {
  text-decoration: line-through;
  color: gray;
  opacity: 0.5;
}
.fall {
  transform: translateY(8rem) rotateZ(15deg);
  opacity: 0;
}
[type="checkbox"]:not(:checked),
[type="checkbox"]:checked {
}
.empty {
  font-size: 1.5rem;
  color: gray;
  opacity: 0.5;
  margin-top: 3rem;
}
.hidden {
  display: none;
}
@media (prefers-color-scheme: dark) {
  body {
    background: #1b1b1b !important;
    color: white !important;
  }
  .todo-item {
    background: #292929 !important;
    color: white !important;
  }
  .header-input input {
    background: #292929 !important;
    color: white !important;
  }
  .header-input button {
    background: #292929 !important;
  }
  .fa-trash {
    color: white !important;
    opacity: 0.5 !important;
  }
  .fa-plus-square {
    color: white !important;
  }
  .fa-plus-square:hover {
    color: #2ca54a !important;
    transition: all 0.5s ease;
  }
}
</style>
