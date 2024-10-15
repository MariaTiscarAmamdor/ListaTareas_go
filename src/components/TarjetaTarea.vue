<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    tarea: {
        type: Object,
        required: true
    }
});
// const emit = defineEmits(['borrarTareaTarjeta']);
</script>

<template>
    <div class="tarjeta_tarea">
        <input type="checkbox" v-model="tarea.hecho">        
        <span><strong>CATEGORÍA:</strong> {{ tarea.cat }}</span>
        <span><strong>DESCRIPCIÓN:</strong> {{ tarea.texto }}</span>
         <!--$ indica que es un método de Vue y no una propiedad o método personalizado.        
        Si se intenta llamar a emit sin el prefijo $, Vue no lo reconocería como un método del framework
         y buscaría una función llamada emit en el contexto actual del componente  -->
        <button @click="$emit('borrarTareaTarjeta', tarea.id)"><img src="../assets/basura.png"></button>
    </div>
</template>

<style scoped>
.tarjeta_tarea {
    display: flex;
    /* justify-content: space-between; */
    /* align-items:center;  */
    margin: 10px 50px;
    background-color: #4CAF50;
    color: white;
    padding: 12px;   
    font-size: 16px;
    text-transform: uppercase;
}

input {
    margin-right: 10px;
    align-items: flex-start;
}

span {
    margin: 0 ;
    padding: 10px;
    color: black;
    text-align: left;
}

button {
    padding: 10px 30px;
    margin-left: 35px;
    align-items: flex-end;
    /* background-color: #4CAF50; */
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease, transform 0.2s ease;
    width: fit-content;
}

button:hover {
    background-color: #c6140b;
    transform: scale(1.05);
}
</style>