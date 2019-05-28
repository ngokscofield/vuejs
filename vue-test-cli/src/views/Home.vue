<template>
  <div id="app">    
    <AddTodo v-on:add-todo="addTodo"/>
    <Todo v-bind:todos="todos" v-on:del-todo1="deleteTodo"/>
  </div>
</template>

<script>
import Header from '../components/layout/Header.vue'
import Todo from '../components/Todo.vue'
import AddTodo from '../components/AddTodo.vue'
import axios from 'axios'
export default {
  name: 'Home',
  components: {
    Todo,
    Header,
    AddTodo
  },
  data(){
    return {
      todos:[
        {
          id:1,
          title:'Todo one',
          completed: true
        }
      ]
    }
  },
  methods:{
    deleteTodo(id){
      axios.delete('https://jsonplaceholder.typicode.com/todos/${id}')
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console(err));
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo){
      const{title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err))
      //this.todos = [...this.todos, newTodo];
    }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
body{
  margin:0px;
  padding:0px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
