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
      <span v-if="option == 'all'" class="text-blue-400 font-bold">All</span>
      <span v-else>All</span>
      <span v-if="option == 'active'" class="text-blue-400 font-bold">Active</span>
      <span v-else>Active</span>
      <span v-if="option == 'completed'" class="text-blue-400 font-bold">Completed</span>
      <span v-else>Completed</span>
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
  },
  option: {
    type: String
  }
})
const { count, option } = toRefs(props)
</script>
