<template >
  <li>
    <span>{{ task.id }} : {{ task.name }}</span>
    <button @click="$emit('removeTask' , task.id)">Eliminar</button>
  </li>
</template>


<script setup>
defineProps(['task']);
</script>
