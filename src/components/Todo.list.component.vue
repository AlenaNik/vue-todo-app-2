<template>
  <div class="hello">
    <input type="text"
           class="todo-input"
           placeholder="What needs to be done?"
           v-model="newTodo"
           @keyup.enter="addTodo"
    >
    <div v-for="todo in todos" :key="todo.id" class="todo-item">
      {{ todo.title }}
    </div>
  </div>
</template>

<script>
export default {
    name: 'Todo',
    data() {
      return {
        newTodo: '',
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
        alert('adding')
      }
  }
  };
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

</style>
