<template>
  <ul class="todo-list">
    <app-todo-item 
      v-for="todo in todos" 
      :key="todo.id" 
      :todo="todo" 
      @toggle-todo="toggleTodoHandler(todo.id)"
      @remove-todo="removeTodoHandler(todo.id)"
    />
  </ul>
</template>
  
<script lang="ts">
import { PropType, defineComponent } from 'vue'
import AppTodoItem from './AppTodoItem.vue'
import { ITodo } from '@/types/todo';

export default defineComponent({
  name: 'app-todo-list',
  components: {
    AppTodoItem
  },
  props: {
    todos: {
      type: Array as PropType<ITodo[]>,
      required: true
    }
  },
  methods: {
    toggleTodoHandler(id: number) {
     this.$emit('toggleTodo', id)
    },
    removeTodoHandler(id: number) {
      this.$emit('removeTodo', id)
    }
  },
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  }
})
</script>

