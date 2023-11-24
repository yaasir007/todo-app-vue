<script setup>
import { ref, defineProps } from 'vue'
const props = defineProps(['editedTitle', 'editedTaskIndex'])

const newTitle = ref("")
</script>

<template>
  <div class="modal fade" id="exampleModalToggle" aria-hidden="true" aria-labelledby="exampleModalToggleLabel" tabindex="-1">
    <div class="modal-dialog modal-dialog-centered">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalToggleLabel">Edit Task - {{ editedTitle }}</h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Add new title" v-model="newTitle">
        </div>
        <div class="modal-footer">
          <button class="btn btn-warning" @click="$emit('closeModal')">Cancel</button>
          <button class="btn btn-primary" @click="$emit('saveChanges', newTitle, editedTaskIndex)">Save Change</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>