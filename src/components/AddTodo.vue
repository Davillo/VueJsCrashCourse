<template>
    <div>
        <form @submit="addTodo">
            <input type="text" id="title" v-model.trim="title" name="title" placeholder="Nome da tarefa">
            <input type="submit" value="Adicionar" class="btn">
        </form>
    </div>
</template>

<script>
import uuid from 'uuid';
export default {
    name: "AddTodo",
    data(){
        return {
            title: ''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault();
           var title = document.getElementById('title'); 
           if(title.value != ''){
                title.value = null;
                const newTodo = {
                id: uuid.v4(),
                title: this.title,
                completed: false
            }

            this.$emit('add-todo',newTodo);
           }
            
        }
    }
}
</script>

<style scoped>
 form{
     display: flex;
 }
 input[type="text"]{
     flex: 10;
     padding: 5px;
 }

 input[type="submit"]{
     flex: 2;
 }
</style>

