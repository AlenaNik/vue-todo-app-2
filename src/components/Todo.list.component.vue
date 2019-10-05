<template>
  <div class="hello">
    <input type="text"
           class="todo-input"
           placeholder="What needs to be done?"
           v-model="newTodo"
           @keyup.enter="addTodo"
    >
    <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item">
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

   <div class="extra-container">
      <div><label><input type="checkbox" :checked="!anyRemaining"
      @change="checkAllTodos">
          Check All
        </label>
      </div>
     <div>{{ remaining }} items left</div>
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
      beforeEditCache: '',
      todos: [
        {
          'id': 1,
          'title': 'Finish tutorial',
          'completed': false,
          'editing': false,
        },
        {
          'id': 2,
          'title': 'Take over world',
          'completed': false,
          'editing': false,
        },
        {
          'id': 3,
          'title': 'Feed a cat and take over world',
          'completed': false,
          'editing': false,
        },
      ]
    }
  },
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.completed).length
    },
    anyRemaining() {
      return this.remaining !== 0
    },
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
    }
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
    editTodo(todo) {
      this.beforeEditCache = todo.title
      todo.editing = true
    },
    doneEdit(todo) {
      todo.editing = false
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    },
    checkAllTodos() {
      this.todos.forEach((todo) => todo.completed = event.target.checked)
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
  border: 1px solid gainsboro;
  border-radius: 5px;

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
.todo-item-left {
  display: flex;
  align-items: center;
}
  .todo-item-label {
    padding: 10px;
    border: 1px solid white;
    margin-left: 12px;
  }
.todo-item-edit {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  font-size: 15px;
  margin-left: 12px;
  width: 100%;
  padding: 10px 18px;
  border: 1px solid gainsboro;
  border-radius: 5px;
  &:focus {
    outline: none;
  }
}

.completed {
  text-decoration: line-through;
  color: lightslategray;
}

.extra-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  border-top: 1px solid lightgray;
  padding-top: 14px;
  margin-bottom: 14px
}

  button {
    font-size: 14px;
    background-color: white;
    appearance: none;

    &:hover {
      background: lightgreen;
    }
    &:focus {
      outline: none;
    }
  }
  .active {
    background: lightgreen;
  }

</style>
