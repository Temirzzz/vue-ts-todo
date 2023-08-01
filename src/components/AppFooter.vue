<template>
  <footer class="app-footer">{{ stats.active }} more to do, {{ stats.done }} done</footer>
</template>

<script lang="ts">
import { PropType, defineComponent } from 'vue'

export interface Stats {
  active: number,
  done: number
}

export default defineComponent({
  name: 'app-footer',
  props: {
    stats: {
      type: Object as PropType<Stats>,
      required: true
    }
  }
})
</script>
