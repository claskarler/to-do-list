<script setup>
import ToDoList from './components/To-do-list.vue';

const ipcHandle = () => window.electron.ipcRenderer.send('ping')
</script>

<template>
  <To-do-list />
</template>
