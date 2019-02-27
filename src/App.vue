<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header.vue'; // cabeçalho componente
import Todos from './components/Todos.vue'; // todos componente que possui o TodoItem dentro dele
import AddTodo from './components/AddTodo.vue';// Componente AddTodo que tem o form e botão

export default {
  name: 'app',
  components: {
    Header, //cabeçalho
    Todos,  // lista
    AddTodo // form e botãoi
  },
  data() {
    return {
     todos: [ //array de objetos com os todos exibidos na tela.
       {
         id: 1,
         title: 'Todo One',
         completed: true
       },
         {
         id: 2,
         title: 'Todo Two',
         completed: false
         },
      {
         id: 3,
         title: 'Todo Three',
         completed: true
      }
     ]
    }
  },
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo){
      this.todos  = [...this.todos, newTodo];
    }
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial,Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn:hover{
  background: #666;
}

.btn{
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
</style>
