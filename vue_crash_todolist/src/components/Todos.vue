<template>
  <div>
    <div :key="todo.id" v-for="todo in todos">
      <TodoItem :todo="todo" @del-todo="$emit('del-todo', todo.id)" @complete-todo="$emit('complete-todo', todo.id)" />
      
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "todos",
  components: {
    TodoItem,
  },
  props: ["todos"],
};
</script>

<style scoped>
</style>