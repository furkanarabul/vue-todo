<template>
<form>
<div class="header-input">
    <input type="text" class="todo-input" placeholder="Write a new task"  v-model="newTodo" @keyup.enter="addTodo">
    <button class="todo-button" type="submit">
        <i class="fas fa-plus-square"></i>
    </button>   
    
</div>
<div v-for="todo in todos" :key="todo.id" class="todo-item">
    {{todo.title}}
</div>
</form>

</template>

<script>
export default {
    name:'todo-list',
    data () {
        return {
            newTodo: '',
            todos:[
                {
                    'title':'Finish Vue Screencast',
                },
                {
                    'title':'Take over world',
                },
            ]
        }
    },
    methods: {
        addTodo(){
            this.todos.push({
                title: this.newTodo,
            })
            this.newTodo = ''
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
</style>

