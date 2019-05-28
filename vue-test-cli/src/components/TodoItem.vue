<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">
            {{todo.title}}
            <button @click="$emit('del-todo2', todo.id)" 
            
            class="del">X</button>
        </p>
    </div>
</template>
<script>
export default {
    name : "TodoItem",
    props:["todo"],
    methods:{
        markComplete(){
            this.todo.completed = !this.todo.completed;
            //console.log(123);
        }
    }
}
</script>
<style scoped>
.todo-item{
    padding: 10px;
}
.is-complete{
    text-decoration: line-through;
}
</style>


