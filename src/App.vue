<script setup>
import { ref, computed } from 'vue'
import Header from '@/components/Header.vue'
import Task from '@/components/Task.vue'
import Menu from '@/components/Menu.vue'

const newTodo = ref('')
const optionSelected = ref('all')
const TODOS = ref([])
const TODOdisplayed = ref([...TODOS.value])

const countTODOS = computed(() => TODOS.value.filter((item) => !item.completed).length)

const markCompleted = (id) => {
  const index = TODOS.value.findIndex((item) => item.id === id)
  if (index !== -1) {
    TODOS.value[index].completed = !TODOS.value[index].completed
  }
}
const changeOption = (option) => {
  optionSelected.value = option
  if (option === 'all') {
    TODOdisplayed.value = [...TODOS.value]
  } else if (option === 'active') {
    const actives = TODOS.value.filter((item) => !item.completed)
    TODOdisplayed.value = [...actives]
  } else {
    const noactives = TODOS.value.filter((item) => item.completed)
    TODOdisplayed.value = [...noactives]
  }
}
const insertTODO = (event) => {
  const key = event.key
  if (key === 'Enter' && newTodo.value.trim()) {
    const data = {
      id: crypto.randomUUID(),
      completed: false,
      todo: newTodo.value
    }
    TODOS.value.push(data)
    newTodo.value = ''
    changeOption(optionSelected.value)
  }
}
const clearTODOS = () => {
  const clear = TODOS.value.filter((item) => item.completed === false)
  TODOS.value = [...clear]
  changeOption(optionSelected.value)
}
</script>

<template>
  <div class="w-full h-screen flex flex-col items-center bg-black">
    <div class="w-full h-40 bg-blue-400 grid place-content-center">
      <div class="max-w-md w-full">
        <Header />
        <input
          class="max-w-md min-w-full bg-[#25273c] py-2 px-5 rounded-sm text-gray-300"
          type="text"
          placeholder="Create a new TODO..."
          v-on:keydown="insertTODO"
          v-model="newTodo"
        />
      </div>
    </div>
    <main class="w-full flex justify-center relative">
      <section class="max-w-md w-full absolute -top-6 p-2">
        <Task
          v-for="item in TODOdisplayed"
          :id="item.id"
          :todo="item.todo"
          :completed="item.completed"
          :key="item.id"
          @markCompleted="markCompleted"
        />
        <Menu
          :count="countTODOS"
          :option="optionSelected"
          @changeOption="changeOption"
          @clearTODOS="clearTODOS"
        />
      </section>
    </main>
  </div>
</template>

<style></style>
