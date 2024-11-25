<script setup>
 import { ref } from 'vue';

  const newTodo = defineModel('newTodo')
  const todos = ref([])

  const addTodo = () => {
    todos.value.push({ title: newTodo.value, completed: false, id: Date.now()})
    newTodo.value = ""
  }
  const removeTodo = (todo) => {
    todos.value = todos.value.filter(t => t != todo)
  }
</script>

<template>
  <form action="" @submit.prevent="addTodo">
    <input type="text" v-model="newTodo">
    <input type="submit" value="add a new todo">
  </form>
  <p v-if="todos.length === 0"> you have any todo currently </p>
  <ul>
    <li :class="{completed: todo.completed}" v-for="todo in todos" :key="todo.id">
      {{ todo.title }}
      <button @click="removeTodo(todo)">delete</button>
      <button @click="todo.completed = true">check</button>
    </li>
  </ul>
</template>

<style scoped>
    .completed{
      opacity: 0.4;
    }
</style>
