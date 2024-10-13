<script setup>
import { ref, computed } from 'vue';
import Formulario from './components/Formulario.vue';
import Tabla from './components/Tabla.vue';

let id = 0;

const tareaCompletada = ref(false);
const tareas = ref([
  { id: id++, texto: ' HTML', cat: 'front-end', hecho: true },
  { id: id++, texto: 'Learn JavaScript', cat: 'front/back-end', hecho: true },
  { id: id++, texto: 'Learn Vue', cat: 'front-end', hecho: false }
]);

function handleAddTarea({ cat, descripcion }) {
  tareas.value.push({ id: id++, texto: descripcion, cat: cat, hecho: false });
}

function borrarTarea(tarea) {
  tareas.value = tareas.value.filter((t) => t !== tarea);
}

const filtroTareas = computed(() => {
  return tareaCompletada.value
    ? tareas.value.filter((t) => !t.hecho)
    : tareas.value;
});

function toggleCompleto() {
  tareaCompletada.value = !tareaCompletada.value;
}
</script>

<template>
  <header>
    <h1>Lista de tareas</h1>
  </header>
  <main>
    <!--  -->
    <Formulario @addTarea="handleAddTarea" />
    <button id="boton_mostrar" @click="toggleCompleto">
      {{ tareaCompletada ? 'Mostrar todas las tareas' : 'Mostrar tareas sin hacer' }}
    </button>
    <!-- directivas para utilizar métodos -->
    <Tabla :tareas="filtroTareas" :borrarTarea="borrarTarea" />
  </main>
</template>

<style scoped>
h1 {
  color: #388e3c;
  text-align: center;
  font-size: 3vw;
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
#boton_mostrar {
  margin-left: 10%;
  background-color: #388e3c;
}
</style>
