<script setup>
import { onMounted, onUpdated, ref } from 'vue'
import { toast } from 'vue3-toastify';
import 'vue3-toastify/dist/index.css';
import taskItem from './components/TaskItem.vue'
import ModalItem from './components/ModalItem.vue'
import TaskInput from './components/TaskInput.vue'
import bootstrap from 'bootstrap/dist/js/bootstrap.js'

const editedTitle = ref('');
const editedTaskIndex = ref();
const tasks = ref([]);
const uncompleted = ref(0);
let Modal;

const notify = (params) => {
  toast(params, {
    autoClose: 1500,
  });
}

const addTask = (task) => {
  tasks.value.push(task)
  notify("Task Added!")
}

const UncompletedTasks = () => {
  uncompleted.value = tasks.value.filter(task => task.completed === false).length
}

const deleteTask = (index) => {
  tasks.value.splice(index, 1)
  updateLocalStorage();
  notify("Task Deleted!")
}

const toggleCompleted = (task) => {
  if (task.completed) {
    task.completed = false
    notify("Undo Task!")
  } else {
    task.completed = true
    notify("Task Completed!")
  }
  UncompletedTasks()
  updateLocalStorage();
}

const updateLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value));
};

const showModal = (task, index) => {
  editedTaskIndex.value = index
  editedTitle.value = task.title
  Modal.show();
}

const saveChanges = (newTitle, editedTaskIndex) => {
  tasks.value[editedTaskIndex].title = newTitle
  notify("Task Updated!")
  updateLocalStorage();
  Modal.hide();
}

const closeModal = () => {
  Modal.hide();
}

onUpdated(() => {
  updateLocalStorage();
  UncompletedTasks()
})

onMounted(() => {
  Modal = new bootstrap.Modal(document.getElementById('exampleModalToggle'))

  const tasksFromLocalStorage = JSON.parse(localStorage.getItem('tasks'));
  if (tasksFromLocalStorage) {
    tasks.value = tasksFromLocalStorage;
  }
})
</script>

<template>
  <div class="container-md mt-5">
    <div class="mb-3">
      <h4 class="mb-3">Uncompleted Todos: <span class="incomplete">{{ uncompleted }}</span></h4>
      <h4 for="exampleFormControlInput1" class="form-label">New Task</h4>
      <TaskInput @addTask="addTask" />
    </div>

    <taskItem v-for="(task, index) in tasks" :tasks="tasks" :task="task" :index="index" :editTask="editTask" v-on:deleteItem="deleteTask" v-on:toggleCompletedItem="toggleCompleted" v-on:editItem="showModal" />

    <ModalItem :editedTitle="editedTitle" :editedTaskIndex="editedTaskIndex" v-on:saveChanges="saveChanges" v-on:closeModal="closeModal" />
  </div>
</template>

<style scoped>

</style>
