<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button class="button" v-for="item in filters" :key="item" :class="{ 'button--primary': activeFilter === item }" @click="filterHandler(item)">{{ item }}</button>
    </section>
  </aside>
</template>
  
<script lang="ts">
import { filter } from '@/types/filter';
import { PropType, defineComponent } from 'vue'

interface State {
  filters: filter[]
}

export default defineComponent({
  name: 'app-filters',
  data(): State {
    return {
      filters: ['Active', 'All', 'Done']
    }
  },
  props: {
    activeFilter: {
      type: String as PropType<filter>,
      required: true
    }
  },
  methods: {
    filterHandler(filter: filter) {
      console.log(filter);
      this.$emit('setFilter', filter)
    }
  },
  emits: {
    setFilter: (filter: filter) => filter
  }
})
</script>
