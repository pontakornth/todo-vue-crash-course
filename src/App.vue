<template>
<main>
  <div class="tabs">
    <div class="tab active">All</div>
    <div class="tab">Active</div>
    <div class="tab">Completed</div>
  </div>
  <div class="todo-list">
    <div class="todo-menu">
      <input class="todo-input" name="todo-title" />
      <button class="primary">Add Todo</button>
    </div>
    <todo-item v-for="todo in todos" :key="todo.id" :todo="todo" />
  </div>
</main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TodoItem from "./components/TodoItem.vue"

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
      ]
    }
  },
  methods: {},
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
