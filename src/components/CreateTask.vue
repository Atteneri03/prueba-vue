<template>
   <p>
  <input type="text" placeholder="nueva tarea" 
  @keyup.enter="$emit('insertTask' , newTask)" 
  
  v-model="newTask">
 </p>
</template>
<!-- @keyup.enter="$emit('insertTask' , newTask)"  -->

<script setup>
import {ref} from 'vue';
// const emit = defineEmits(['insertTask'])

const newTask = ref('');

function insertTask(){
  // console.log("nueva tarea en componente: " + newTask.value);
  if(newTask.value.length>2){
    $emit('insertTask' ,newTask.value);
    newTask.value = "";
  }

}

</script>


<style scoped>
  p {
    background-color:lightblue;
    padding: 20px;
  }
</style>