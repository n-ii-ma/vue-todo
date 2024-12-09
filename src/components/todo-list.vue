<script setup lang="ts">
import { computed } from "vue";

import type { Todo } from "@/types/types";

// https://vuejs.org/guide/typescript/composition-api.html#complex-prop-types
// defineProps({
//   todos: Array as PropType<Todo[]>,
// });

// Define props
const props = defineProps<{
  todos: Todo[];
  toggleCompleted: (id: string) => void;
  deleteTodo: (id: string) => void;
}>();

// Update the remaining todos count based on their incompleted status
const remainingTodos = computed(() => props.todos.filter((todo) => !todo.completed).length);
</script>

<template>
  <h1>Remaining Todos: {{ remainingTodos }}</h1>
  <div v-if="todos.length">
    <div v-for="todo in todos" :key="todo.id" class="flex items-center gap-2">
      <input @click="toggleCompleted(todo.id)" type="checkbox" name="completed" id="completed" />
      <h2 v-if="todo.completed" class="line-through opacity-50">{{ todo.text }}</h2>
      <h2 v-else>
        <strong>{{ todo.text }}</strong>
      </h2>
      <button @click="deleteTodo(todo.id)">x</button>
    </div>
  </div>
  <h2 v-else>Nothing to show</h2>
</template>
