<template>
<main>
  <div class="tabs">
    <div class="tab active">All</div>
    <div class="tab">Incomplete</div>
    <div class="tab">Complete</div>
  </div>
  <div class="todo-list">
    <div class="todo-menu">
      <input class="todo-input" v-model="todoInputText" name="todo-title" />
      <button @click="addTodoItem" class="primary">Add Todo</button>
    </div>
    <todo-item @remove="onRemoveTodoItem" @toggle="onToggleTodoItem" v-for="todo in visibleTodos" :key="todo.id" :todo="todo" />
  </div>
</main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { nanoid } from "nanoid"
import TodoItem, { Todo } from "./components/TodoItem.vue"

type ViewState = 'all' | 'incomplete' | 'complete'

export default defineComponent({
  name: 'App',
  data() {
    return {
      todos:  [
        {
          task: "Fighting gold",
          isComplete: false,
          id: "reiktirkit"
        },
        {
          task: "Find traitor requiem",
          isComplete: true,
          id: "eiluriedkiki"
        }
      ] as Todo[],
      todoInputText: "",
      viewState: 'all' as ViewState
    }
  },
  computed: {
    visibleTodos() {
      switch (this.viewState) {
        case 'complete':
          return this.todos.filter(todo => todo.isComplete)
        case 'incomplete':
          return this.todos.filter(todo => !todo.isComplete)
        default:
          return this.todos
      }
    }
  },
  methods: {
    addTodoItem() {
      this.todos.push({
        id: nanoid(),
        task: this.todoInputText,
        isComplete: false
      })
    },
    removeTodoItem(id: string) {
      this.todos = this.todos.filter(todo => todo.id !== id)
    },
    onRemoveTodoItem(event: Partial<Todo>) {
      this.removeTodoItem(event.id!!)
    },
    toggleTodoItem(id: string) {
      this.todos = this.todos.map(todo => todo.id === id ? {...todo, isComplete: !todo.isComplete} : todo)
    },
    onToggleTodoItem(event: Partial<Todo>) {
      this.toggleTodoItem(event.id!!)
    }
  },
  components: {
    TodoItem
  }
})
</script>

<style>
* {
  box-sizing: border-box;
}
main {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  min-width: 80%;
  max-width: 90%;
  margin: auto;
  padding: 2rem;
}
.primary {
  color: white;
  background: blue;
  border: none;
  cursor: pointer;
}
.accent {
  color: white;
  background: red;
  border: none;
  cursor: pointer;
}
.tabs {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  text-align: center;
  cursor: pointer;
}
.tab {
  padding: .55rem;
  background: white;
  text-decoration: underline;
  color: blue;
  border: 1px solid blue;
}
.tab.active {
  color: white;
  background: blue;
}
.todo-input {
  flex: 1;
}
.todo-list {
  padding: 1rem;
  display: flex;
  flex-flow: column nowrap;
  justify-content: space-evenly;
  align-items: center;
  border: 1px solid blue;
}
.todo-menu {
  display: flex;
  justify-content: space-between;
  flex-flow: row nowrap;
  width: 100%;
}
</style>
