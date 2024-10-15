<script setup>
import { defineProps } from 'vue';
// Propiedades para recibir los datos del componente padre, en este caso slice tareas y
// metodo borrarTarea
const props = defineProps(['tareas', 'borrarTarea']);
</script>

<template>
  <h2>Lista de tareas</h2>
  <table>
      <thead>
        <tr>        
          <th>Categoría</th>
          <th>Descripción</th>
          <th>Marcar como Hecha</th>
          <th>Borrar</th>
        </tr>
      </thead>
      <tr v-for="tarea in tareas" :key="tarea.id">     
        <td><span>{{ tarea.cat }}</span></td>
        <td><span>{{ tarea.texto }}</span></td>
        <td><input type="checkbox" v-model="tarea.hecho"></td>
        <td><button @click="borrarTarea(tarea)"><img src="../assets/basura.png"></button></td>
      </tr>
    </table>
</template>

<style scoped>
h2 {
  color: #388e3c;
  text-align: center;
  font-size: 2vw;
}
table {
  margin: 20px auto;
  border-collapse: collapse;
  width: 80%;
  background-color: #f9f9f9;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  overflow: hidden;
}

table th {
  background-color: #4CAF50;
  color: white;
  padding: 12px;
  text-align: left;
  font-size: 16px;
  text-transform: uppercase;
}


table td {
  padding: 12px;
  border-bottom: 1px solid #ddd;
  text-align: left;
  color: #333;
}


table tr:nth-child(even) {
  background-color: #f2f2f2;
}


table tr:hover {
  background-color: #e0f7fa;
  cursor: pointer;
}


table td:last-child {
  text-align: center;
  color: #666;
}

table button {
  padding: 10px 30px;  
  background-color: #388e3c;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s ease, transform 0.2s ease;
  width: fit-content;

}

table button:hover {  
  transform: scale(1.05);

}
</style>
