<script setup lang="ts">
// Define model and change its argument to `title`
const title = defineModel<string>("title");

// Define props
defineProps<{
  addTodo: () => void;
}>();
</script>

<template>
  <form @submit.prevent="addTodo" class="space-x-2">
    <input v-model="title" type="text" required class="border border-gray-400 p-1 rounded-md" />
    <button type="submit" class="bg-gray-400 border border-gray-400 p-1 rounded-md">Add</button>
  </form>
</template>
