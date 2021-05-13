<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addTodo">
    <label>Add a Todo</label><br />
    <input name="newTodo" v-model="newTodo" /><br />
    <button>Submit</button><br />  
  </form>
    <button @click="markAllDone">Mark All Done</button>
    <button @click="removeAll">Remove All</button>
   <ul>
      <li v-for="(item, index) in todos" :key="item.id" class="todo">
        <h3 :class="{ done: item.done }" @click="toggleDone(item)">
          {{ item.content }}
        </h3>
        <button @click="removeTodo(index)">Remove Todo</button>
      </li>
    </ul>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");

    const todos = ref([]);

    function addTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(item) {
      item.done = !item.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone(){
      todos.value.forEach((item) => item.done = true);
    }

    function removeAll(){
      todos.value = ([]);
    }

    return {
      removeAll,
      markAllDone,
      removeTodo,
      toggleDone,
      todos,
      addTodo,
      newTodo,
    };
  },
};
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 1.5em;
  margin: 0 auto;
  width: 90%;
}
input,
button,
p,
div {
  display: block;
  width: 100%;
  font-family: sans-serif;
  margin: 0.5em;
}
.done {
  text-decoration: line-through;
}
.todo {
  cursor: pointer;
}
</style>
