<template>
    <div id="app">
        <h1>To do application</h1>
        <hr />
        <router-vue />
    </div>
</template>

<script>
import ToDoList from "@/components/ToDoList";
import AddTodo from "@/components/AddTodo";
export default {
    name: "App",
    data() {
        return {
            todos: [
                //     { id: 1, title: "to buy", completed: false },
                //     { id: 2, title: "to read", completed: true },
                //     { id: 3, title: "to go", completed: false },
            ],
        };
    },
    mounted() {
        fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
            .then((response) => response.json())
            .then((json) => (this.todos = json));
    },
    methods: {
        removeTodo(id) {
            this.todos = this.todos.filter((t) => t.id !== id);
        },
        addTodo(todo) {
            this.todos.push(todo);
        },
    },
    components: {
        ToDoList,
        AddTodo,
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
