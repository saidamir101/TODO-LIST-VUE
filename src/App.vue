<script setup>

</script>

<template>
  
  <div>
<div><p class="text-center text-4xl mt-4 font-bold text-[blue] font-mono">{{ title }}</p></div>

<div class="">
  <div class="flex justify-center mt-5">
      <input type="number" placeholder="Search by ID" v-model="searchId" class="w-40 px-3 py-2 rounded-md border border-gray-400">
    </div>
  <div class="justify-center  mt-10 flex gap-5">
  <input type="" v-model="text" placeholder="I can do" class="outline-none w-[420px] h-[40px] rounded-lg px-3 border border-black ">
  <button @click="addTodo(id++)" class="bg-[black] w-[100px] text-white h-[40px] rounded-lg" >Add</button>
</div>
  <div class="bg-gray-100  border-[green] border rounded-lg px-2 w-[35%]  mt-2 mx-auto  " v-for="todo in this.filteredTodos" :key="todo.id">
    <div class="flex justify-center items-center p-2 gap-10 ">  
      <span class="todo__id bg-[red]  text-white text-center px-2  rounded-xl"  >{{ todo.id }}</span>
  
      <span  v-if="!editting"  class="todo__text " :class="{todo__text_isDone:isDone}" >{{ todo.text }}</span>
      <input v-bind:value="editText" @change="editTextChange" v-else type="text">
      <div  class="flex items-center gap-2">
      <input type="checkbox" class="inline-block todo_check" v-model="isDone" >
      <button @click="deleteTodo(todo.id)" class="bg-[green] px-2 text-white rounded">delete</button>
      <button @click="editTodo(todo)" class="bg-[red] px-2 text-white rounded">{{editting?"update":"edit"}}</button>
    </div>
    </div>
 

  </div>

</div>
  </div>
</template>
<script>
import {mapActions} from "vuex"
export default {
  data(){
    return {
      title:"Todo List",
      text:"",
      todos:[],
      isDone:false,
      id:0,
      editting:false,
      editText:"",
      searchId: null
    }
  },
  computed: {
    filteredTodos() {
      if (!this.searchId) {
        return this.todos;
      }

      return this.todos.filter((todo) => todo.id === this.searchId);
    },
  },
  methods:{
    ...mapActions(["deleteTodo","editTodo"]),
    addTodo(){
      if(this.text.trim().length == 0){
        alert("please add todo")
      }
      else{
           this.todos.push({
        id:this.id,
        text:this.text,
        done:this.isDone
    }),
      this.text=""
      }
   
    },
    filteredTodos() {
      if (!this.searchId) {
        return this.todos;
      }

      return this.todos.filter((todo) => todo.id === parseInt(this.searchId));
    },
    //delete
    deleteTodo(id){
      console.log(id);
let del = this.todos.filter((e)=>{
  console.log(e.id);
  return e.id != id
}) 
   this.todos.pop(del)   },
   //edit
   editTextChange(e){
    this.editText= e.target.value
   },
   editTodo(todo){
this.editting = this.editting == true ? false:true
if(this.editting){
  this.editText = todo.text
  let index = this.todos.findIndex((e)=>e.id == todo.id)

}
else{
  todo.text = this.editText
}

   }
 
    
  }
}
</script>
<style lang="scss">
.todo{
  border: 2px solid gray;
  &__text{
 &_isDone{
  text-decoration: line-through;
 }
  }

}

</style>