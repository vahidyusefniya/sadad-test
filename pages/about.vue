<script setup lang="ts">
import { ref } from 'vue'
import { useInfiniteScroll } from '@vueuse/core'

const el = ref<HTMLElement | null>(null)
const data = ref([1, 2, 3, 4, 5, 6])

useInfiniteScroll(
  el,
  () => {
    // load more
    data.value.push(data.value.length + 10)
  },
  { distance: 10 }
)
</script>

<template>
  <div ref="el" style="height: 300px; overflow-y: scroll">
    <div v-for="item in data">
      {{ item }}
    </div>
  </div>
</template>