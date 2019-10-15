<template>
  <div class="hello">
    <input type="text"
           class="todo-input"
           placeholder="What needs to be done?"
           v-model="newTodo"
           @keyup.enter="addTodo"
    >
    <todo-item v-for="(todo, index) in todosFiltered" :key="todo.id" :todo="todo" :index="index">
    </todo-item>

   <div class="extra-container">
      <div><label><input type="checkbox" :checked="!anyRemaining"
      @change="checkAllTodos">
          Check All
        </label>
      </div>
     <div>{{ remaining }} to-do left</div>
   </div>

    <div class="extra-container">
     <div>
       <button :class="{ active: filter == 'all' }"
       @click="filter = 'all'">All</button>
       <button :class="{ active: filter == 'active'}"
               @click="filter = 'active'">Active</button>
       <button :class="{ active: filter == 'completed'}"
               @click="filter = 'completed'">Completed</button>
     </div>
      <div>
       <button class="clear" v-if="showClearCompletedButton" @click="clearCompleted">Clear Completed</button>
      </div>
    </div>

  </div>
</template>

<script>
import TodoItem from './TodoItem.component';

export default {
  name: 'Todo',
  components: { TodoItem },
  component: 'TodoItem',
  data() {
    return {
      newTodo: '',
      idForTodo: 4,
      beforeEditCache: '',
      filter: 'all',
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
    todosFiltered() {
      if (this.filter === 'all') {
        return this.todos
      } else if (this.filter === 'active') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'completed') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    },
    showClearCompletedButton() {
      return this.todos.filter(todo => todo.completed).length > 0
    }
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
    },
    clearCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed)
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
    border-radius: 5px;
    padding: 10px;

    &:hover {
      background: #42b983;
      color: white;
    }
    &:focus {
      outline: none;
    }
  }
  .active {
    background: #42b983;
    color: white;
  }
.clear {
    background-color: pink;
  }

</style>
