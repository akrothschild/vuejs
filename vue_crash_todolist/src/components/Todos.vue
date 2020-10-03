<template>
  <div>
    <div v-for="todo in todos" :key="todo.id">
      <TodoItem
        :todo="todo"
        @del-todo="$emit('del-todo', todo.id)"
        @complete-todo="$emit('complete-todo', $event)"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  components: {
    TodoItem,
  },
  props: ["todos"],
  methods: {},
};
</script>

<style scoped>
</style>