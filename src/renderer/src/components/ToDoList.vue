<script setup>
  import { ref } from 'vue';
  import ListItem from './ListItem.vue';

  const listItems = ref([])
  const showItemForm = ref(0)
  const newItem = ref("");
  
function addListItem() {
  if (newItem.value.trim()) {
    listItems.value.push({text: newItem.value, done: false});
    newItem.value = ""; 
    showItemForm.value = false; 
  }
}

  function toggleForm() {
  showItemForm.value = !showItemForm.value;
}

function toggleDone(index) {
  listItems.value[index].done = !listItems.value[index].done;
}
</script>

<template>
  <div class="app-container h-100"> 
    <div class="d-flex justify-content-center align-items-center py-3">
      <div class="d-flex justify-content-between list-title bg-white p-3">
        <i class="bi bi-star"></i>
        <span class="mx-3">TO DO</span>
        <i class="bi bi-star"></i>
      </div>
    </div>
    <div class="to-do-list-container bg-white mx-3 d-flex flex-column">
      <ul class="d-flex flex-column list-unstyled">
        <ListItem
          v-for="(item, index) in listItems" 
          :key="index" 
          :item="item"
          @toggle-done="toggleDone(index)"
        />
      </ul>

      <button v-if="!showItemForm" @click="toggleForm" class="align-self-center new-item-btn mb-2">+</button>

      <div v-if="showItemForm" class="new-item-form d-flex align-items-center m-3">
        <input v-model="newItem" type="text" placeholder="Write something..." />
        <button @click="addListItem" class="align-items-center">Add</button>
      </div>
    </div>
  </div>
</template>
