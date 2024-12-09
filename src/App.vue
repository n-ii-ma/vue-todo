<script setup lang="ts">
import { ref } from "vue";
import { nanoid } from "nanoid";

import TodoList from "./components/todo-list.vue";
import TodoForm from "./components/todo-form.vue";

import type { Todo } from "./types/types";

// State
const todos = ref<Todo[]>([]);
const todoTitle = ref<string>("");

/** Callback to add a new todo */
const addTodo = () => {
  const newTodo: Todo = {
    id: nanoid(),
    text: todoTitle.value,
    completed: false,
  };

  todos.value.push(newTodo);
  todoTitle.value = "";
};

/** Callback to toggle the completed status of a todo */
const toggleCompleted = (id: string) => {
  const foundTodo = todos.value.find((todo) => todo.id === id);

  if (foundTodo) {
    foundTodo.completed = !foundTodo.completed;
  }
};

/** Callback to delete a todo */
const deleteTodo = (id: string) => {
  const todoIndex = todos.value.findIndex((todo) => todo.id === id);
  todos.value.splice(todoIndex, 1);
};
</script>

<template>
  <main class="flex flex-col items-center justify-center gap-3 h-svh w-full">
    <TodoList :todos="todos" :toggle-completed="toggleCompleted" :delete-todo="deleteTodo" />
    <TodoForm v-model:title="todoTitle" :add-todo="addTodo" />
  </main>
</template>
