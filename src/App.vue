<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <input name="newTodo" v-model="newTodo">
    <button>Add New Todo</button>
  </form>
  <button @click="markAllDone">Mark All Done</button>
  <button @click="removeAllTodos">Remove All</button>
  <ol>
    <li :class="{ done: todo.done }" v-for="(todo, index) in todos" :key="todo.id">
   <h3 @click="toggleDone(todo)">{{ todo.content }}</h3>
   <button @click="removeTodo(index)">Remove Todo</button>
 </li>
  </ol>
 
</template>

<script>
import { ref } from 'vue';

export default {
  setup(){
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo(){
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,

      });
      newTodo.value = '';
    }

    function toggleDone(todo){
      todo.done = !todo.done;
    }

    function removeTodo(index){
      todos.value.splice(index, 1);
    }

    function markAllDone(){
      todos.value.forEach((todo) => todo.done = true);
    }

    function removeAllTodos(){
todos.value = [];
    }

    return{
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  }
}
</script>

<style>

body{
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
input, textarea, button, p, div, section, article, select{
  display: block;
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}
.done{
  text-decoration: line-through;
}
h3{
  cursor: pointer;
}
</style>
