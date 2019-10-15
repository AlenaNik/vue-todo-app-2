<template>
<div class="todo-item">
  <div class="todo-item-left">
    <input type="checkbox" v-model="completed">
    <div v-if="!editing" @dblclick="editTodo"
         class="todo-item-label" :class="{ completed : completed}">{{ title }}</div>
    <input v-else class="todo-item-edit"
           type="text"
           v-model="title"
           @blur="doneEdit"
           @keyup.enter="doneEdit"
           v-focus
           @keyup.esc="cancelEdit"
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
  },
  data() {
    return {
      'id': this.todo.title,
      'title': this.todo.title,
      'completed': this.todo.completed,
      'editing': this.todo.editing,
      'beforeEditCache': '',
    }
  }
}
</script>
<style>

</style>
