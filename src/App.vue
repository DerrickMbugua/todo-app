<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <input name="newTodo" v-model="newTodo">
    <button>Add New Todo</button>
  </form>
 <h2> {{ newTodo }} </h2>
</template>

<script>
import { ref } from 'vue';

export default {
  setup(){
    const newTodo = ref('');


    function addNewTodo(){
      console.log('form was submitted');
    }
    return{
      newTodo,
      addNewTodo,
    };
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
