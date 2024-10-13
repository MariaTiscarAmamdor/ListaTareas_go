<script setup>
import { defineProps } from 'vue';
const props = defineProps(['toggleHecho']);
</script>

<template>
    <button id="boton_mostrar" @click="toggleHecho">
        {{ tareaCompletada ? 'Mostrar todas las tareas' : 'Mostrar tareas sin hacer' }}
    </button>
</template>
<style scoped>
#boton_mostrar {
    margin-left: 10%;
    background-color: #388e3c;
}
button {
  padding: 10px 30px;
  margin-left: 15px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s ease, transform 0.2s ease;
  width: fit-content;
}

button:hover {
  background-color: #388e3c;
  transform: scale(1.05);
}
</style>