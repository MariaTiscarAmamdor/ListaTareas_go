<script setup>
import { ref, computed } from 'vue';
import CrearTarea from './components/CrearTarea.vue';
import ListaTarea from './components/ListaTarea.vue';
// import Mostrar from './components/Mostrar.vue';

let id = 0;


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
function borrarTarea(id) {
  console.log(id)
  tareas.value = tareas.value.filter((t) => t.id !== id);
}


</script>

<template>
  <header>
    <h1>Aplicacion de tareas</h1>
  </header>
  <main>
    <!--  -->
    <CrearTarea @addTarea="anadirTarea" />
    <!-- <Mostrar :toggleHecho="toggleHecho"/>  -->
    <h2>Lista de tareas</h2>
    <ListaTarea :tareas="tareas" @borrarTareaTarjeta="borrarTarea"/>
  </main>
</template>

<style scoped>
template{
  margin: 20px auto;
  width: 80%;
  background-color: #f9f9f9;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  overflow: hidden;
}
h1 {
  color: #388e3c;
  text-align: center;
  font-size: 3vw;
}
h2 {
  color: #388e3c;
  text-align: center;
  font-size: 2vw;
}
</style>
