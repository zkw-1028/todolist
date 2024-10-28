<script setup>
import ToDoHeader from "./components/ToDoHeader.vue";
import ToDoMain from "./components/ToDoMain.vue";
import ToDoFooter from "./components/ToDoFooter.vue";
import {computed, ref} from 'vue'
const list = ref([
  { id: 1,name:'晨练',done:false},
  { id: 2,name:'练书法',done:true},
])
const addTodo = (name)=>{
  list.value.push({name,done:false,id:~~(Math.random()+1000)})
}
const delTodo = (id) =>{
  list.value = list.value.filter(item => item.id !== id)
}
const lastLength = computed(()=>{
  return list.value.filter(item => !item.done).length
})
const status = ref('all')
const showList = computed(()=>{
  if (status.value === 'all'){
    return list.value
  }else if (status.value === 'active'){
    return list.value.filter(item => !item.done)
  }else if(status.value === 'completed'){
    return list.value.filter(item => item.done)
  }
})
const updateStatus = statusData=>{
  status.value = statusData
}
</script>

<template>
  <ToDoHeader @addTodo="addTodo"></ToDoHeader>
  <ToDoMain :list="showList" @delTodo="delTodo" ></ToDoMain>
  <ToDoFooter :lastLength="lastLength" :status="status" @updateStatus="updateStatus"></ToDoFooter>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
