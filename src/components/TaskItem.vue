<script setup>
const props = defineProps(['tasks', 'task', 'index'])
</script>

<template>
  <ul class="list-group">
    <li v-if="task.completed" class="list-group-item mb-2 list-item opacity-50">
        <div class="d-flex justify-content-between align-items-center">
            <div>
              <span class="ms-2" :class="{ 'text-decoration-line-through': task.completed }">{{ task.title }}</span>
            </div>
            <div class="d-flex justify-content-space-between">
              <button v-if="task.completed" class="btn btn-sm btn-warning mx-1" @click="$emit('toggleCompletedItem', task)">undo</button>
              <button v-else class="btn btn-sm btn-success mx-1" @click="$emit('toggleCompletedItem', task)">Completed</button>

              <!-- <button class="btn btn-sm btn-primary mx-1" @click="$emit('editItem', task, index)">Edit</button> -->
              <button class="btn btn-sm btn-danger mx-1" @click="$emit('deleteItem', index)">Delete</button>
            </div>
        </div>
    </li>
    <li v-else class="list-group-item mb-2 list-item opacity-100">
        <div class="d-flex justify-content-between align-items-center">
            <div>
              <span class="ms-2" :class="{ 'text-decoration-line-through': task.completed }">{{ task.title }}</span>
            </div>
            <div class="d-flex justify-content-space-between">
              <button v-if="task.completed" class="btn btn-sm btn-warning mx-1" @click="$emit('toggleCompletedItem', task)">undo</button>
              <button v-else class="btn btn-sm btn-success mx-1" @click="$emit('toggleCompletedItem', task)">Completed</button>

              <button class="btn btn-sm btn-primary mx-1" @click="$emit('editItem', task, index)">Edit</button>
              <button class="btn btn-sm btn-danger mx-1" @click="$emit('deleteItem', index)">Delete</button>
            </div>
        </div>
    </li>
  </ul>
</template>

<style scoped>
</style>
