<template>
    <div>
        <h2>To do application</h2>
        <router-link to="/">Home</router-link>
        <hr />
        <h6>Clear input field after submit</h6>
        <h6>Fix NAN problem if index</h6>

        <AddTodo @add-todo="addTodo" />
        <hr />
        <ToDoList
            v-if="todos.length"
            v-bind:todos="todos"
            @remove-todo="removeTodo"
        />
        <p v-else>No todos!</p>
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
