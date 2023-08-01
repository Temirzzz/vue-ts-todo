<template>
  <section class="add-todo">
    <form class="add-todo__form" v-if="isAddFormVisible" @submit.prevent="addTodo">
      <button class="close-button" type="button" @click.stop="closeAddFormHandler">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input class="input" v-model="todoText" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button"  @click="addFormVisibleHandler">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>
  
<script lang="ts">
import { ITodo } from '@/types/todo'
import { defineComponent } from 'vue'

interface State {
  isAddFormVisible: boolean,
  todoText: string
}

export default defineComponent({
  name: 'app-add-todo',
  data(): State {
    return {
      isAddFormVisible: false,
      todoText: ''
    }
  },
  methods: {
    addFormVisibleHandler() {
      this.isAddFormVisible = true
    },
    closeAddFormHandler() {
      this.isAddFormVisible = false
    },
    addTodo() {
      this.$emit('addTodo', {
        id: Date.now(),
        text: this.todoText,
        isCompleted: false
      })
      this.todoText = ''
    }
  },
  emits: {
    addTodo: (todo: ITodo) => todo
  }
})
</script>
  
