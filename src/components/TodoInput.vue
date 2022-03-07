<template>
  <div id="container">
    <!-- <h2><strong>{{ name }}</strong></h2> -->
    <div class="container">
      <div class="row">
        <form action="">
          <div class="form-group">
              <div class="">
                  <input type="text" class="form-control" placeholder="todos ..." aria-invalid="false" v-model="todo" @keyup.enter="addTodo">
                  <button class="btn btn-primary" type="button" @click="addTodo">Add Todo</button>
              </div>
          </div>
        </form>
      </div>
    </div>
  
    <todo-list :key="reRender"/>
  </div>
</template>

<script lang="ts">
const baseURL = 'http://localhost:3000/todos';
import { defineComponent } from 'vue';
import  TodoList  from './TodoList.vue';

export default defineComponent({
  name: 'ExploreContainer',
  props: {
    name: String
  },
  components : {
    "todo-list" : TodoList
  },
  data (){
    return {
      todo : '',
      reRender : 0
    }
  },
  methods :{
    
    async addTodo(){
      try {
        let response = await fetch(baseURL, {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json;charset=utf-8'
          },
          body: JSON.stringify({todo:this.todo})
        });
        this.todo = ''
        this.reRender ++;
        alert("todo saved")
      } catch (error) {
        console.log(error);
        
      }
     
    }

  }
});
</script>

<style scoped>
#container {
  text-align: center;
  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}
.form-control{
  width: 70% !important;
  display: inline;
}
#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;
  color: #8c8c8c;
  margin: 0;
}

#container a {
  text-decoration: none;
}
</style>
