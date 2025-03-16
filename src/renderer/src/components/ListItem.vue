<script setup>
defineProps({
  item: Object
});

const emit = defineEmits(["toggle-done"]);
</script>

<template>
  <li class="list-item d-flex justify-between align-items-center">
    <button class="done-button" @click="emit('toggle-done')">
      <i :class="item.done ? 'bi bi-heart-fill' : 'bi bi-heart'"></i>
    </button>
    <span :class="{ 'text-decoration-line-through': item.done }">
      {{ item.text }}
    </span>
  </li>
</template>
