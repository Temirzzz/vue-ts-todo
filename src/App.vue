<template>
  <app-header />
  <app-filters :active-filter="activeFilter" @set-filter="setFilterHandler" />
  <main class="app-main">
    <app-todo-list :todos="filteredTodos" @remove-todo="removeTodoHandler" @toggle-todo="toggleTodoHandler"/>
    <app-add-todo @add-todo="addTodoHandler" />
  </main>
  <app-footer :stats="stats" />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppHeader from '@/components/AppHeader.vue'
import AppFilters from '@/components/AppFilters.vue'
import AppTodoList from '@/components/AppTodoList.vue'
import AppAddTodo from '@/components/AppAddTodo.vue'
import AppFooter, { Stats } from '@/components/AppFooter.vue'
import { ITodo } from './types/todo'
import { filter } from './types/filter'

interface State {
  todos: ITodo[],
  activeFilter: filter
}

export default defineComponent({
  components: {
    AppHeader,
    AppFilters,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  data(): State {
    return {
      todos: [
        { id: 1, text: 'Learn the basics of Vue', isCompleted: true },
        { id: 2, text: 'Learn the basics of Typescript', isCompleted: false },
        { id: 3, text: 'Subscribe to the channel', isCompleted: false },
      ],
      activeFilter: 'All'
    }
  },
  computed: {
    filteredTodos(): ITodo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodods
        case 'Done':
          return this.doneTodos
        case 'All':
        default:
          return this.todos
      }
    },
    stats(): Stats {
      return {
        active: this.activeTodods.length,
        done: this.doneTodos.length
      }
    },
    activeTodods(): ITodo[] {
      return this.todos.filter(todo => !todo.isCompleted)
    },
    doneTodos(): ITodo[] {
      return this.todos.filter(todo => todo.isCompleted)
    }
  },
  methods: {
    addTodoHandler(todo: ITodo) {
      console.log(todo);
      this.todos.push(todo)
    },
    toggleTodoHandler(id: number) {
      const nessesaryTodo = this.todos.find((todo: ITodo) => todo.id === id)
      if(nessesaryTodo) nessesaryTodo.isCompleted = !nessesaryTodo.isCompleted
    },
    removeTodoHandler(id: number) {
      this.todos = this.todos.filter((todo: ITodo) => todo.id !== id)
    },
    setFilterHandler(filter: filter) {
      this.activeFilter = filter
    }
  }
})
</script>