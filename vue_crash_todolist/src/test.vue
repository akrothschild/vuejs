<template>
  <div id="App">
    <Header />
    <AddTodo @add-todo="addTodo" />
    <Todos
      :todos="todos"
      @del-todo="deleteTodo"
      @complete-todo="completeTodo"
    />
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    Todos,
    AddTodo,
  },
  data() {
    return {
      isChecked: true,
      post: null,
      todos: [],
    };
  },
  methods: {
    toggleCheck() {},
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/users/1/todos/${id}`)
        .then((this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
    completeTodo(todoId) {
      let todo = this.todos.find((todo) => todo.id === todoId);

      console.log(todo.completed);

      todo.completed = !todo.completed;

      console.log(todo.completed);
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post("https://jsonplaceholder.typicode.com/users/1/todos", {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/users/1/todos?_limit=5")
      .then((res) => {
        this.todos = res.data;
      })
      .catch((err) => console.log(err));
    // fetch("https://jsonplaceholder.typicode.com/users/1/todos")
    //   .then((response) => response.json())
    //   .then((json) => console.log(json));
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
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
