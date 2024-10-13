<script setup>
import { ref, computed } from 'vue';
import Formulario from './components/Formulario.vue';
import Tabla from './components/Tabla.vue';
import Mostrar from './components/Mostrar.vue';

let id = 0;

const tareaCompletada = ref(false);
const tareas = ref([
  { id: id++, texto: ' HTML', cat: 'front-end', hecho: true },
  { id: id++, texto: 'Learn JavaScript', cat: 'front/back-end', hecho: true },
  { id: id++, texto: 'Learn Vue', cat: 'front-end', hecho: false }
]);
//funcion de añadir tarea al slice tareas 
function anadirTarea({ cat, descripcion }) {
  tareas.value.push({ id: id++, texto: descripcion, cat: cat, hecho: false });
}
//funcion de borrar tarea
function borrarTarea(tarea) {
  tareas.value = tareas.value.filter((t) => t !== tarea);
}
//funcion para filtrar del slice de tareas según en función del valor de tareaCompletada true/false
const filtroTareas = computed(() => {
  return tareaCompletada.value
    ? tareas.value.filter((t) => !t.hecho)
    : tareas.value;
});
//funcion para alternar el valor de tareaCompletada entre true y false.
function toggleHecho() {
  tareaCompletada.value = !tareaCompletada.value;
}
</script>

<template>
  <header>
    <h1>Lista de tareas</h1>
  </header>
  <main>
    <!--  -->
    <Formulario @addTarea="anadirTarea" />
    <Mostrar :toggleHecho="toggleHecho"/>   
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

</style>
