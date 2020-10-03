<template>
  <div id="App">
    <Header />
    <AddTodo @add-todo="addTodo" />
    <Todos
      :todos="todos"
      @del-todo="deleteTodo"
      @complete-todo="completeTodo"
    />

    <!-- <input type="checkbox" :checked="isChecked" @up /> -->

    <!-- <ul>
      <li v-for="number in numbers" :key="number">
        {{ number }}
      </li>
    </ul> -->
  </div>
</template>

<script>
import Header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";

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
      numbers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 0],
      todos: [
        {
          id: 1,
          title: "Todo One",
          completed: false,
        },
        {
          id: 2,
          title: "Todo Two",
          completed: true,
        },
        {
          id: 3,
          title: "Todo Three",
          completed: false,
        },
      ],
    };
  },
  methods: {
    toggleCheck() {},
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    completeTodo(todoId) {
      let todo = this.todos.find((todo) => todo.id === todoId);

      console.log(todo.completed);

      todo.completed = !todo.completed;

      console.log(todo.completed);
    },
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },
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
