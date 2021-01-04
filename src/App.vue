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
          :key="todo.id"
          class="todo-item"
          :class="{ completed: todo.completed }"
        >
          {{ todo.title }}
          <input
            type="checkbox"
            v-model="todo.completed"
            class="complete-btn"
            @click="completeTodo(index)"
          />
          <button @click="removeTodo(todo)" class="trash-btn">
            <i class="fas fa-trash"></i>
          </button>
        </li>
      </ul>
    </div>
    <div class="github">
      <a
        href="https://github.com/furkanarabul/vue-todo"
        target="_blank"
        title="to-do app"
      >
        <i class="fab fa-github fa-2x"></i>
      </a>
    </div>
  </div>
</template>

<script>
import axios from "axios";
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
        this.$alert("New task cannot be empty.", "", "warning");
        return;
      }
      axios
        .post(
          "https://vue-todo-437fb-default-rtdb.firebaseio.com/todoList.json",
          { title: this.newTodo, completed: false }
        )
        .then((response) => {
          this.todos.push({
            id: response.data.name,
            title: this.newTodo,
            completed: false,
          });
          this.newTodo = "";
        })
        .catch((e) => {
          console.log(e);
        });
    },
    removeTodo(todo) {
      if (event.target.classList.contains("fa-trash")) {
        event.target.parentElement.parentElement.classList.add("fall");
      }
      axios
        .delete(
          "https://vue-todo-437fb-default-rtdb.firebaseio.com/todoList/" +
            todo.id +
            ".json"
        )
        .then((response) => {
          //console.log(response);
          let index = this.todos.findIndex((i) => {
            return i.id == todo.id;
          });
          this.todos.splice(index, 1);
        })
        .catch((e) => {
          console.log(e);
        });
    },
    completeTodo(index) {
      axios.patch(
        "https://vue-todo-437fb-default-rtdb.firebaseio.com/todoList/" +
          this.todos[index].id +
          ".json",
        { completed: !this.todos[index].completed }
      );
    },
  },
  created() {
    axios
      .get("https://vue-todo-437fb-default-rtdb.firebaseio.com/todoList.json")
      .then((response) => {
        for (let key in response.data) {
          //console.log(response.data[key].title)
          //console.log(response.data)
          let todo = {
            title: response.data[key].title,
            completed: response.data[key].completed,
            id: key,
          };
          this.todos.push(todo);
        }
      })
      .catch();
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
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
ul {
  padding: 20px;
}
a {
  text-decoration: none;
  color: inherit !important;
  opacity: 0.2;
}
a:hover {
  opacity: 1;
  transition: all 0.5s ease;
}

.todo-item {
  background: white;
  padding: 0rem 0.5rem;
  margin-top: 1rem;
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
  zoom: 1.8;
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
.github {
  position: fixed;
  top: 15px;
  right: 15px;
}
.popover {
  color: rgb(212, 68, 68);
  padding: 10px;
  margin: 10px;
  border-radius: 8px;
  border: 1px solid rgba(121, 121, 121, 0.5);
}
@media (prefers-color-scheme: dark) {
  body {
    background: #1b1b1b !important;
    color: white !important;
  }
  a {
    color: gray !important;
    opacity: 0.5 !important;
  }
  a:hover {
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
    z-index: -1;
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
