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
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header, //cabeçalho
    Todos,  // lista
    AddTodo // form e botãoi
  },
  data() {
    return {
     todos: [] //array de objetos com os todos exibidos na tela.]
    }
  },
  methods:{
    deleteTodo(id){

      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`). // delete request
      then(res => this.todos = this.todos.filter(todo => todo.id !== id)) //atualização do array
      .catch(err => console.log(err)); // tratamento da promise
    
    },
    addTodo(newTodo){

      const {title, completed}  = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos',{ //post request
        title,
        completed
      }).
      then(res => this.todos  = [...this.todos, res.data]) // atualizando com o retorno do post
      .catch(err => console.log(err));// tratamento da promise
      
    }
  },
  created(){

    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5') //get request
    .then(res => this.todos = res.data) //atualiza o array com os TODOS da API
    .catch(err => console.log(err)); // tratamento da promise
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
