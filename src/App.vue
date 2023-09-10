<script setup>
import { ref, computed, onMounted } from 'vue';
  let id = 0;
const todos = ref([
  { id: id++, text: 'gg', done: false },
  { id: id++, text: 'YY', done: false },
  { id: id++, text: 'RR', done: false }
])

const newTodo = ref('');
const hideCompleted = ref(false);
const addTodo = () => {
  todos.value.push({ id: id++, text: newTodo.value })
  newTodo.value = '';
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter(t => t !== todo)
  todo.done = !todo.done
}

const toggleCompleted = () => {
  hideCompleted.value = !hideCompleted.value;
}

const filteredTodos = computed(() => {
  return hideCompleted.value ?
    todos.value.filter((todo) => !todo.done) :
    todos.value
})
</script>

<template>
  <div>
    <h1>v-for computed todolist</h1>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo">
      <button>Add todo</button>
    </form>
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.done">
        <span :class="{ 'text-with-underline': todo.done }">{{ todo.text }} id:{{todo.id}}</span>
        <button @click="removeTodo(todo)">X</button>
      </li>
    </ul>
    <button @click="toggleCompleted">{{ hideCompleted ? 'Show All' : 'Hide Completed' }}</button>
  </div>
</template>

<style scoped>
.text-with-underline {
  text-decoration: line-through;
}
</style>
