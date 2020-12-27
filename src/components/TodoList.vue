<template>
<div>
    <div class="header-input">
        <input type="text" class="todo-input" placeholder="Write a new task"  v-model="newTodo" @keyup.enter="addTodo">
        <button @click="addTodo" class="todo-button">
            <i class="fas fa-plus-square"></i>
        </button>
    </div>
    <div class="todo-list">
        <ul>
            <li v-for="todo in todos" :key="todo.title" class="todo-item">
                {{todo.title}}
                <button @click="checkTodo" class="complete-btn"><i class="fas fa-check"></i></button>
                <button @click="removeTodo" class="trash-btn"><i class="fas fa-trash"></i></button>
            </li>
        </ul>
    </div>
</div>
</template>

<script>
export default {
    name:'todo-list',
    data () {
        return {
            newTodo: '',
            todos:[
            ]
        }
    },
    methods: {
        addTodo(){
            this.todos.push({
                title: this.newTodo,
                completed: false,
            })
            this.newTodo = ''
        },
        removeTodo(){
            alert('remove')
        },
        checkTodo(){
            alert('check')
        }
    }
}
</script>

<style>
.header-input {
    display: flex;
    border-radius: 18px;    
    display: flex;
    justify-content: center;
    align-items: center;
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
.todo-item{
    background: white;
    padding: 0rem 0.5rem;
    margin:1rem;
    height: 60px;
    color:black;
    font-size:1.5rem;
    display: flex;
    align-items: center;
    transition: all 0.5s ease;
    border-radius: 8px;
}
.complete-btn{
    margin-left: auto;
    background: none;
}
.trash-btn{
    background:none;
}
.trash-btn:hover{
    color:rgb(212, 68, 68);
}

</style>

