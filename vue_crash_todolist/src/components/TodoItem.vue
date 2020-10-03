<template>
  <div class="todo-item" :class="{ 'is-complete': todo.completed }">
    <p>
      <input
        type="checkbox"
        :checked="todo.completed"
        @change="$emit('complete-todo', todo.id)"
      />
      {{ todo.title }}
      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </p>
  </div>
</template>
      
<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {},
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  border-bottom: 1 px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>