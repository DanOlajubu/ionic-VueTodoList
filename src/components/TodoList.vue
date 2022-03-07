<template>
  <div class="container">
      <div class="panel panel-primary">
        <div class="panel-heading">Todo List</div>
        <div class="panel-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="todo in todos" :key="todo.id">{{todo.todo}}
                <span class="del" @click="deleteTodo(todo.id)">X</span>
              </li>
            </ul>
        </div>
    </div>
  </div>
</template>

<script>
const baseURL = 'http://localhost:3000/todos';
export default {
  data(){
    return {
      todos : []
    }
  },
  methods : {
    async deleteTodo(id){
      try {
        let response = await fetch(baseURL+'/'+id, {
          method: 'DELETE',
          headers: {
            'Content-Type': 'application/json;charset=utf-8'
          },
          body: JSON.stringify({todo:this.todo})
        });
        this.$router.go()
        alert("todo deleted")
      } catch (error) {
        console.log(error);
        
      }
    }
  },
 created  (){
   fetch(baseURL)
  .then(response => response.json())
  .then(data => this.todos = data);
  
  }
}
</script>

<style scoped>
.del{
  color:red; 
  float:right; 
  border:1px solid red;
  border-radius: 5px;
  padding: 0px 5px;
}
.del:hover{
  color:white;
  background: red;
}
</style>