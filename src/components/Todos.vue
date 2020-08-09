<template>
<div>
    <div v-bind:key="todo.id" v-for="todo in todos">
        <!-- this enables us to loop through the props -->
        <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)"/>
    </div>
    <!-- need to have a unique key every time you loop, otherwise it will show an error -->
      <!-- v-on: is used for events(such as a change event for a checkbox) -->
</div>
    
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
    name: "Todos",
    props: ["todos"], 
    components: {
        TodoItem
        }
    // here we are accepting the todos array as props. This means we can have access to them in the template. 
    // Because the props we are passing through is an array, we need to loop over them in the template, using v-for. 
}
</script>

<style lang="scss" scoped>

</style>