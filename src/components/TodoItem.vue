<template>
  <div class="todo-item">
    <div class="todo-content">
      <input @change="handleToggleTodo" class="todo-checkbox" :checked="todo.isComplete" type="checkbox" name="todo"/>
      {{todo.task}}
    </div>
    <div class="todo-action">
      <button @click="handleRemoveTodo" class="accent">Delete</button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'

export type Todo = {
  task: string,
  isComplete: boolean,
  id: string,
}

export default defineComponent({
  name: "TodoItem",
  methods: {
    handleToggleTodo() {
      this.$emit("toggle", { id: this.todo.id }) 
    },
    handleRemoveTodo() {
      this.$emit("remove", { id: this.todo.id })
    }
  },
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true
    }
  }
})
</script>

<style scoped>
.todo-item {
  padding: 1rem;
  display: flex;
  border: 1px solid blue;
  width: 100%;
  margin-top: 1rem;
  justify-content: space-between;
}
.todo-content {
  text-align: left;
}
</style>