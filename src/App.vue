<template lang="">
  <p style="background-color: pink; padding: 10px;">
    <!-- Opción:
    <select v-model="option">
      <option value="list">Listado</option>
      <option value="create">Crear Tarea</option>
    </select> -->

    <input type="radio" id="list" value="list" v-model="option" />
    <label for="list">Listado</label>

    <input type="radio" id="create" value="create" v-model="option" />
    <label for="create">Crear Tarea</label>
  </p>
  <div v-if ="option=='list'">
 <h1>Lista de tareas</h1>
 <!-- <p>
  <input type="text" placeholder="nueva tarea" @keyup.enter="insertTask" v-model="newTask">
 </p> -->
 <p>Se han encontrado {{tasks.length}} tareas</p>
 <p>{{textoNumeroTareas}}</p>
 <ul>
  <ViewTask v-for="task of tasks" 
  :key = "task.id" 
  :task="task"
   @remove-task = "removeTask"/>
 </ul>
 <ul>
    <li v-for="task of tasks" 
    :key="task.id"
    @click="removeTask(task.id)">
    {{task.id}}  - {{task.name}}
  </li>
 </ul>
</div>
 <CreateTask v-else @insert-task='insertTask'/>
</template>

<script setup>
import { computed, ref } from 'vue';
import CreateTask from './components/CreateTask.vue';
import ViewTask from './components/ViewTask.vue';

const option = ref('list');

const tasks = ref([
  {id: 1, name: 'Corregir examenes del lado del servidor'},
  {id: 2, name: 'Corregir examenes del lado del cliente'},
  {id: 3, name: 'Corregir examenes de recuperación'},
  {id: 4, name: 'Preparar examen chungo de Vue'},
]);

const newTask = ref('');

const textoNumeroTareas = computed(() => {
   if(tasks.value.length == 0) return "No hay tareas";
   else if(tasks.value.length == 1) return "Hay una tarea";
   return "Hay " + tasks.value.length + " tareas.";
});

function insertTask(task){
  tasks.value.push({
    id: newId.value,
    name : task
});
}

const newId = computed(() => {
  const max = Math.max(...tasks.value.map(t => t.id))+1;
  
  return max < 0 ? 1 : max;
});

function removeTask(id){
  tasks.value = tasks.value.filter(t => t.id!==id);
}
</script>

<style lang="">
  
</style>