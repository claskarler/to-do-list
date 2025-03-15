<script setup>
  import { ref } from 'vue';

  const listItem = ref([])
  const showItemForm = ref(0)
  const newItem = ref("");
  
function addListItem() {
  if (newItem.value.trim()) {
    listItem.value.push({text: newItem.value, done: false});
    newItem.value = ""; 
    showItemForm.value = false; 
  }
}

  function toggleForm() {
  showItemForm.value = !showItemForm.value;
}

function toggleDone(index) {
  listItem.value[index].done = !listItem.value[index].done;
}
</script>

<template>
  <div> 
    <h2>TO DO:</h2>
    <ul>
      <li 
        v-for="(item, index) in listItem" 
        :key="index" 
        class="d-flex justify-between align-items-center"
      >
        <button @click="toggleDone(index)">
          <i :class="item.done ? 'bi bi-heart-fill' : 'bi bi-heart'"></i>
        </button>
        <span :class="{ 'text-decoration-line-through': item.done }">{{ item.text }}</span>
      </li>
    </ul>  

    <button @click="toggleForm">+</button>

    <div v-if="showItemForm">
      <input v-model="newItem" type="text" placeholder="Enter item name" />
      <button @click="addListItem">Add</button>
    </div>
  </div>
</template>
