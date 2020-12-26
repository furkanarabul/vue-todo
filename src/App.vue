<template>
  <div id="app" class="container">
    <img class="logo" src="./assets/logo.png">
    <todo-list></todo-list>
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList,
  }
}
</script>

<style>
*{
  box-sizing: border-box;
}
body{
  font-family: "Abel", sans-serif;
  background: rgb(241, 241, 241);
  color: black;
  min-height: 100vh;
  transition: all 0.5s ease;
}
input{
  padding: 1rem;
  font-size: 1.5rem;
  border: none;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}
.container{
  max-width: 720px;
  margin: 0 auto;
}
.logo{
  display: block;
  margin: 20px auto;
  height: 75px  ;
}
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
