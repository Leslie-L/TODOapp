<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <section
    class="max-w-md w-full shadow-md bg-slate-50 dark:text-white dark:bg-[#25273c] p-2 rounded-b-md flex justify-between text-sm"
  >
    <div>
      <span v-if="count <= 1">{{ count }} item left</span>
      <span v-else>{{ count }} items left</span>
    </div>
    <div class="flex gap-2 items-center">
      <span v-if="option == 'all'" class="text-blue-400 font-bold">All</span>
      <span
        v-else
        @click="changeOptionSelected('all')"
        class="hover:text-blue-600 hover:scale-105 hover:font-semibold"
        >All</span
      >
      <span v-if="option == 'active'" class="text-blue-600 font-bold">Active</span>
      <span
        v-else
        @click="changeOptionSelected('active')"
        class="hover:text-blue-400 hover:scale-105 hover:font-semibold"
        >Active</span
      >
      <span v-if="option == 'completed'" class="text-blue-600 font-bold">Completed</span>
      <span
        v-else
        @click="changeOptionSelected('completed')"
        class="hover:text-blue-400 hover:font-semibold hover:scale-105"
        >Completed</span
      >
    </div>
    <div class="text-right">
      <span @click="clear" class="hover:text-blue-400 hover:font-semibold hover:scale-105"
        >Clear Completed</span
      >
    </div>
  </section>
</template>
<script setup>
import { defineProps, toRefs, defineEmits } from 'vue'

const props = defineProps({
  count: {
    type: Number
  },
  option: {
    type: String
  }
})
const { count, option } = toRefs(props)
const emits = defineEmits(['changeOption', 'clearTODOS'])

const changeOptionSelected = (option) => {
  emits('changeOption', option)
}
const clear = () => {
  emits('clearTODOS')
}
</script>
