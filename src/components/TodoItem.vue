<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <input type="checkbox" v-on:change="markComplete">
           {{todo.title}}
        <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </div>
</template>
<script>
export default {
    name: "TodoItem",
    props: ["todo"], 
    methods: {
        markComplete(){
           this.todo.completed = !this.todo.completed;
         }
    }
}
</script>

<style scoped>

    .todo-item {
        background: #f4f4f4; 
        padding: 10px;
        border-bottom: 1px #ccc dotted;
        margin-left: 2%;
        margin-right: 2%;
    }

.del {
  background: #ff0000; 
  color: #fff; 
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
.is-complete {
    text-decoration: line-through;
}
</style>