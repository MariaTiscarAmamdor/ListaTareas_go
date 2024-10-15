<script setup>
import { ref, computed, defineProps } from 'vue';
import TarjetaTarea from './TarjetaTarea.vue';

const props = defineProps({
    tareas: {
        type: Array,
        required: true
    }
});

//funcion de borrar tarea
// function borrarTarea(tarea) {
//   tareas.value = tareas.value.filter((t) => t !== tarea);
// }
const emit = defineEmits(['borrarTareaTarjeta'])
const tareaCompletada = ref(false);
//funcion para filtrar del slice de tareas según en función del valor de tareaCompletada true/false
const filtroTareas = computed(() => {
  return tareaCompletada.value
    ? props.tareas.filter((t) => !t.hecho)
    : props.tareas;
});
//funcion para alternar el valor de tareaCompletada entre true y false.
function toggleHecho() {
  tareaCompletada.value = !tareaCompletada.value;
}
</script>

<template>
<div>
    <TarjetaTarea 
            v-for="tarea in filtroTareas"
            :key="tarea.id"
            :tarea="tarea"
            @borrarTareaTarjeta="$emit('borrarTareaTarjeta', tarea.id)"
        />
</div>
<button id="boton_mostrar" @click="toggleHecho">        
        {{ tareaCompletada ? 'Mostrar tareas sin hacer' : 'Mostrar todas las tareas' }}
    </button>
</template>

<style scoped>
div {
  margin: 20px auto;
  width: 80%;
  background-color: #f9f9f9;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  overflow: hidden;

}
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