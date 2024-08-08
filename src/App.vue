<template>
  <div>
    <h1>Todo List</h1>
    <form @submit.prevent="addNewTodo">
      <label>New todo</label>
      <input v-model="newTodo" name="newtodo">
      <button>Add New todo</button>
    </form>
    <button @click="markAllDone">Mark All Done</button>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h3>
        <button @click="removeTodo(index)">Remove Todo</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach(todo => todo.done = true);
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
    };
  }
};
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>
