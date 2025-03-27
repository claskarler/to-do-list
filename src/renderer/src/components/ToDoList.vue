<script setup>
import { ref, watch } from 'vue'
import ListItem from './ListItem.vue'
import Confetti from './Confetti.vue'

const listItems = ref([])
const listSettings = ref([{
  confettiEnabled: true
}])
const showItemForm = ref(0)
const newItem = ref('')
const allComplete = ref(false)

function addListItem() {
  if (newItem.value.trim()) {
    listItems.value.push({ text: newItem.value, done: false })
    newItem.value = ''
    showItemForm.value = false
  }
}

function clearList() {
  listItems.value = []
}

watch(
  listItems,
  (newList) => {
    allComplete.value = newList.length > 0 && newList.every((item) => item.done)
  },
  { deep: true }
)

function toggleForm() {
  showItemForm.value = !showItemForm.value
}

function toggleDone(index) {
  listItems.value[index].done = !listItems.value[index].done
}
</script>

<template>
  <div class="app-container h-100">
    <Confetti v-if="allComplete && listSettings[0].confettiEnabled" />
    <div class="d-flex justify-content-center align-items-center py-3">
      <div class="d-flex justify-content-between list-title bg-white p-3">
        <i class="bi bi-star"></i>
        <span class="mx-3">TO DO</span>
        <i class="bi bi-star"></i>
      </div>
    </div>
    <div class="to-do-list-container bg-white mx-3 d-flex flex-column">
      <div class="list-top">
        <button class="list-top-btn me-1" data-bs-toggle="modal" data-bs-target="#settingsModal">
          <i class="bi bi-three-dots-vertical"></i>
        </button>
        <button class="list-top-btn" @click="clearList"><i class="bi bi-trash"></i></button>
      </div>
      <ul class="d-flex flex-column list-unstyled">
        <ListItem
          v-for="(item, index) in listItems"
          :key="index"
          :item="item"
          @toggle-done="toggleDone(index)"
        />
      </ul>

      <button v-if="!showItemForm" class="align-self-center new-item-btn mb-2" @click="toggleForm">
        +
      </button>

      <div v-if="showItemForm" class="new-item-form d-flex align-items-center m-3">
        <input v-model="newItem" type="text" placeholder="Write something..." />
        <button class="align-items-center" @click="addListItem">Add</button>
      </div>
    </div>
  </div>

  <div class="modal fade" id="settingsModal" tabindex="-1" aria-labelledby="settingsModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content modal-custom">
      <div class="modal-header">
        <h1 class="modal-title fs-5" id="settingseModalLabel">List settings</h1>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <div class="d-flex">
          <label class="switch me-2">
          <input v-model="listSettings[0].confettiEnabled" type="checkbox">
          <span class="slider"></span>
        </label>
          <p>Confetti on completed list</p>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" data-bs-dismiss="modal">Close</button>
        <button type="button" >Save changes</button>
      </div>
    </div>
  </div>
</div>
</template>
