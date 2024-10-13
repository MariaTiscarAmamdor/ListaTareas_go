<script setup>
import { ref, computed } from 'vue'

let id = 0

const newCat = ref('')
const newDescripcion = ref('')
const tareaCompletada = ref(false)
const todos = ref([
  { id: id++, texto: ' HTML', cat: 'front-end', hecho: true },
  { id: id++, texto: 'Learn JavaScript', cat: 'front-end', hecho: true },
  { id: id++, texto: 'Learn Vue', cat: 'front-end', hecho: false }
])

function addTodo() {
  todos.value.push({ id: id++, texto: newDescripcion.value, cat: newCat.value, hecho: false })
  newCat.value = ''
  newDescripcion.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}

const filtroTareas = computed(() => {
  return tareaCompletada.value
    ? todos.value.filter((t) => !t.hecho)
    : todos.value
})
</script>
<template>
  <header>
    <h1>Lista de tareas</h1>
  </header>
  <main>
    <form @submit.prevent="addTodo">
      <label for="category">Categoría de la Tarea:</label>
      <input id="category" v-model="newCat" required placeholder="Ej. Trabajo, Personal"
        aria-label="Categoría de la Tarea" />
      <label for="description">Descripción de la Tarea:</label>
      <input id="description" v-model="newDescripcion" required placeholder="Describe la tarea..."
        aria-label="Descripción de la Tarea" />
      <button>Añadir</button>
    </form>
    <button id="boton_mostrar"  @click="tareaCompletada = !tareaCompletada">
      {{ tareaCompletada ? 'Mostrar todas las tareas' : 'Mostrar tareas sin hacer' }}
    </button>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Categoría</th>
          <th>Descripción</th>
          <th>Marcar como Hecha</th>
          <th>Borrar</th>
        </tr>
      </thead>
      <tr v-for="todo in filtroTareas" :key="todo.id">
        <td><span>{{ todo.id }}</span></td>
        <td><span>{{ todo.cat }}</span></td>
        <td><span>{{ todo.texto }}</span></td>
        <td><input type="checkbox" v-model="todo.hecho"></td>
        <td><button @click="removeTodo(todo)">X</button></td>
      </tr>
    </table>
  </main>
</template>

<style scoped>
h1 {
  color:  #11a819;
  text-align: center;
  font-size: 3vw;

}

form {
  display: flex;
  flex-direction: row;  
  margin: 20px auto;
  width: 78%;
  align-items: center;  
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);

}

label {
  padding: 20px;
  font-size: 18px;
}


input[type="text"] {
  width: 100%;
  padding: 40px;
  margin: 30px;
  margin-left: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s ease;

}


button {
  padding: 10px 30px;
  margin: 15px;
  margin-left: 30px;
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


table {
  margin: 20px auto;
  border-collapse: collapse;
  width: 80%;
  background-color: #f9f9f9;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  overflow: hidden;
}
#boton_mostrar{
  margin-left: 10%;
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
</style>