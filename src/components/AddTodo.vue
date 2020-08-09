<template>
<div>
    <form @submit="addTodo">
        <input type="text" v-model="title" name="title" placeholder="Add Todo...">
        <input type="submit" value="Submit" class="btn">
    </form>
</div>
    
</template>

<script>
export default {
    name: "AddTodo", 
    data(){
        return {
            title: ''
        }
    }, 
    methods: {
        addTodo(e){
            e.preventDefault();
            const newTodo = {
                title: this.title, 
                completed: false
            }

            this.$emit('add-todo', newTodo);
            // the emit sends this object up the chain to App JS (where the array is) so it can then be added to it

            this.title = '';
        }
    }
}
</script>

<style scoped>
form {
    display: flex;
}

input[type="text"]{
    flex:10; 
    padding: 15px;
    border: none;
    margin-left: 2%;
}

input[type="submit"]{
    flex: 2;
    margin-right: 2%;
}
</style>