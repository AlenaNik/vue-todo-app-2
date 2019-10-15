<template>
<div class="todo-item">
  <div class="todo-item-left">
    <input type="checkbox" v-model="todo.completed">
    <div v-if="!todo.editing" @dblclick="editTodo(todo)"
         class="todo-item-label" :class="{ completed : todo.completed}">{{ todo.title }}</div>
    <input v-else class="todo-item-edit"
           type="text"
           v-model="todo.title"
           @blur="doneEdit(todo)"
           @keyup.enter="doneEdit(todo)"
           v-focus
           @keyup.esc="cancelEdit(todo)"
    >
  </div>
  <div class="remove-items" @click="removeTodo(index)">
    &times;
  </div>
</div>
</template>
<script>
export default {
  name: 'TodoItem',
  props: {
    todo: {
      type: Object,
      required: true,
    },
    index: {
      type: Number,
      required: true,
    }
  }
}
</script>
<style>

</style>
