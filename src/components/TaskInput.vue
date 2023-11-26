<script setup>
import { ref } from 'vue'

const emit = defineEmits(["addTask"])
const newTask = ref("")

const createTask = () => {
  if (newTask.value.trim() !== "") {
    emit('add-task', { title: newTask.value, completed: false })
    newTask.value = ""
  }
}
</script>

<template>
  <input
    type="text"
    v-model="newTask"
    class="form-control mt-3 homeInput"
    id="exampleFormControlInput1"
    placeholder="Press enter to add item..."
    @keyup.enter="createTask"
  />
</template>

<style scoped></style>
