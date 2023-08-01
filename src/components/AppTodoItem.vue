<template>
  <li class="todo-item" :class="{ 'todo-item--done': todo.isCompleted }" @click="toggleTodo">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue'
import { ITodo } from '../types/todo';

export default defineComponent({
  name: 'app-todo-item',
  props: {
    todo: {
      type: Object as PropType<ITodo>,
      required: true
    }
  },
  methods: {
    toggleTodo() {
      // Не мутируем пропсы, поэтому эмитим сам todo на верх и там хендлим
      this.$emit('toggleTodo', this.todo.id)
    },
    removeTodo() {
      this.$emit('removeTodo', this.todo.id)
    }
  },
  // emits: ['toggleTodo'] // можно перечислять эмиты в массиве, но тогда нельзя типизировать аргументы эмита
  emits: {
    toggleTodo: (id: number) => Number.isInteger(id),
    removeTodo: (id: number) => Number.isInteger(id),
  }

})
</script>
