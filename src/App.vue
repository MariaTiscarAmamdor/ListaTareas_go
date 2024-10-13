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
    <button @click="tareaCompletada = !tareaCompletada">
        {{ tareaCompletada ? 'Mostrar todas' : 'Mostrar sin hacer' }}
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
  color: blue;
  text-align: center;
  font-size: 3vw;
}
</style>