<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <section
    class="max-w-md w-full text-white bg-[#25273c] p-2 rounded-b-md flex justify-between text-sm"
  >
    <div>
      <span v-if="count <= 1">{{ count }} item left</span>
      <span v-else>{{ count }} items left</span>
    </div>
    <div class="flex gap-2 items-center">
      <span>All</span>
      <span>Active</span>
      <span>Completed</span>
    </div>
    <div class="text-right">
      <span>Clear Completed</span>
    </div>
  </section>
</template>
<script setup>
import { defineProps, toRefs } from 'vue'

const props = defineProps({
  count: {
    type: Number
  }
})
const { count } = toRefs(props)
</script>
