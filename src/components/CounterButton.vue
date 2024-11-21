<template>
    <div class="container">
        <div class="d-flex justify-content-center align-items-center vh-100"> <!-- Flexbox para centrar -->
            <div class="col-3 text-center"> <!-- Añadir text-center para centrar texto -->
                <h4 :class="getStyle" class="fs-1">Contador: {{ counter }}</h4>
                <div class="d-flex justify-content-center mt-2">
                    <button class="btn btn-primary" @click="handledIncrement"> +1 </button>
                    <button class="btn btn-navy m-2" @click="resett"> Reset </button>
                    <button class="btn btn-primary" @click="handledDecrement"> -1</button>
                </div>
                <hr>
                <button class="btn btn-primary" @click="agregar" :disabled="isDisabled">Agregar</button>
                <div class="bottom-bar">
                    <p v-for="num in addedNumbers" :key="num"> {{ num }} - </p> <!-- Mostrar números agregados -->
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const counter = ref(0); // Variable reactiva
const addedNumbers = ref([]); // Lista para almacenar números agregados
const handledIncrement = () => {
    counter.value += 1; // Incrementa el contador
}

const handledDecrement = () => {
    counter.value -= 1; // Decrementa el contador
}

const resett = () => {
    counter.value = 0; // Resetea el contador
}
const agregar =() =>{
    if (!addedNumbers.value.includes(counter.value)) {
        addedNumbers.value.push(counter.value); // Agrega el número a la lista
    }
}
//variable computada para verificar si el botón debe estar deshabilitado
const isDisabled = computed(() => {
    return addedNumbers.value.includes(counter.value); // Deshabilita si el número ya está en la lista
});

// Variable computada para determinar el estilo del encabezado
const getStyle = computed(() => {
    if (counter.value === 0) return 'text-success';
    if (counter.value > 0) return 'text-primary';
    return 'text-danger'; // Para valores negativos
});
</script>

<style scoped>
.container {
    height: 100vh;
    /* Altura completa de la ventana */
}

button {
    margin: 0 5px;
    /* Espacio entre los botones */
}
.bottom-bar {
    height: 30px; /* Altura de la barra */
    background-color: #343a40; /* Color de fondo */
    color: white; /* Color del texto */
    display: flex;
    align-items: center; /* Centra verticalmente el texto */
    justify-content: center; /* Centra horizontalmente el texto */
    margin-top: 10px; /* Espacio entre el contador y la barra */
}
</style>