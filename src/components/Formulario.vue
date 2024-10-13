<script setup>
import { ref, defineEmits } from 'vue';

// Propiedades y métodos a usar en el formulario
const emit = defineEmits(['addTarea']);
const newCat = ref('');
const newDescripcion = ref('');

//metodo para añadir tarea
function addTarea() {
  emit('addTarea', { cat: newCat.value, descripcion: newDescripcion.value });
  newCat.value = '';
  newDescripcion.value = '';
}

</script>

<template>
<form @submit.prevent="addTarea">
      <label for="categoria">Categoría de la Tarea:</label>
      <input id="categoria" v-model="newCat" required placeholder="Escribe una categoría..."
        aria-label="Categoría de la Tarea" />
      <label for="description">Descripción de la Tarea:</label>
      <input id="description" v-model="newDescripcion" required placeholder="Describe la tarea..."
        aria-label="Descripción de la Tarea" />
      <button>Añadir</button>
    </form>
</template>

<style scoped>

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
  margin-left: 30px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s ease;

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
