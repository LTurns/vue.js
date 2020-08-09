<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    <!-- you have to traverse to the component where the array/data is. This is why we have traversed up from TodoItem etc to App -->
    <!-- The same is done with AddTodo -->
    
  </div>
</template>

<script>
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo'
import axios from 'axios';


export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  }, 
  data(){
    return {
      todos:[]
     }
   }, 
   methods: {
     deleteTodo(id){
       axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        // eslint-disable-next-line
       .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
       .catch(err => console.log(err));
     },
     addTodo(newTodo){
       const { title, completed } = newTodo;

       axios.post('https://jsonplaceholder.typicode.com/todos', {title, completed })
       // eslint-disable-next-line
       .then(res => this.todos = [...res.data])
       .catch(err => console.log(err));
       this.todos = [...this.todos, newTodo];
      //  the spread operator enables you to copy what's already in todos 
      // here we add the newTodo onto the current list of todos.
     }
   },
   created(){
     axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
     .then(res => this.todos = res.data)
    //  this means we are filling our todos array with the content we receive from json (res.data)
     .catch(err => console.log(err));
   }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background-color: black;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
  border: none;
}
</style>

