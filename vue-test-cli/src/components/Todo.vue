<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos">
            <TodoItem v-bind:todo="todo" v-on:del-todo2="$emit('del-todo1', todo.id)"/>
        </div>
    </div>
</template>
<script>
import TodoItem from './TodoItem.vue'
export default {
    name:"Todo",
    components:{
        TodoItem
    },
    props:["todos"]
}
</script>
<style scoped>

</style>


