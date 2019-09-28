<template>
  <div class="hello">
    <input type="text"
           class="todo-input"
           placeholder="What needs to be done?"
           v-model="newTodo"
           @keyup.enter="addTodo"
    >
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
      {{ todo.title }}
      <div class="remove-items" @click="removeTodo(index)">
        &times;
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  data() {
    return {
      newTodo: '',
      idForTodo: 4,
      todos: [
        {
          'id': 1,
          'title': 'Finish tutorial',
          'completed': false,
        },
        {
          'id': 2,
          'title': 'Take over world',
          'completed': false,
        },
        {
          'id': 3,
          'title': 'Feed a cat and take over world',
          'completed': false,
        },
      ]
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim().length === 0) {
        return
      }
      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false,
      })
      this.newTodo = ''
      this.idForTodo++
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.todo-input {
  width: 100%;
  padding: 10px 18px;
  font-size: 10px;
  margin-bottom: 16px;

  &:focus {
    outline: 0;
  }
}

  .todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .remove-items {
    cursor: pointer;
    margin-left: 14px;
    &:hover {
      color: hotpink;
    }
  }

</style>
