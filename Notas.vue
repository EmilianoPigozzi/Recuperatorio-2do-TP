
<script setup>
import { ref } from 'vue'

var materia = ref('')
var fecha = ref('')
var nota = ref('')
var error = ref('')
var notas = ref([])

function agregarNota() {
  error.value = ''

  if (materia.value == '' || fecha.value == '' || nota.value == '') {
    error.value = 'Completa todos los campos'
  } else if (nota.value < 1 || nota.value > 10) {
    error.value = 'La nota debe ser un numero del 1 al 10'
  } else {
    notas.value.push({
      materia: materia.value,
      fecha: fecha.value,
      nota: Number(nota.value)
    })

    materia.value = ''
    fecha.value = ''
    nota.value = ''
  }
}

function eliminarNota(i) {
  notas.value.splice(i, 1)
}
</script>

<template>
  <div class="contenedor">
    <h1>Mis Notas</h1>

    <label>Materia</label>
    <input v-model="materia" placeholder="Nombre de la materia">

    <label>Fecha</label>
    <input v-model="fecha" type="date">

    <label>Nota</label>
    <input v-model="nota" type="number" min="1" max="10" placeholder="Del 1 al 10">

    <button @click="agregarNota">Agregar nota</button>

    <p v-if="error" class="error">{{ error }}</p>

    <h2>Mis calificaciones</h2>

    <p v-if="notas.length == 0">Todavia no hay notas.</p>

    <div
      v-for="(item, i) in notas"
      :key="i"
      :class="item.nota >= 7 ? 'verde' : 'rojo'"
      class="nota"
    >
      <h3>{{ item.materia }}</h3>
      <p>Fecha: {{ item.fecha }}</p>
      <p>Nota: {{ item.nota }}</p>

      <p v-if="item.nota >= 7">Aprobado</p>
      <p v-else>Desaprobado</p>

      <button @click="eliminarNota(i)">Eliminar</button>
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
  background-color: #111318;
  font-family: Arial, sans-serif;
  color: white;
}

.contenedor {
  max-width: 500px;
  margin: 30px auto;
  padding: 25px;
  background-color: #222530;
  border-radius: 10px;
}

h1 {
  text-align: center;
  color: #42b883;
}

label {
  display: block;
  margin-top: 15px;
}

input {
  width: 100%;
  padding: 10px;
  margin-top: 5px;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 12px;
  margin-top: 15px;
  background-color: #42b883;
  border: none;
  cursor: pointer;
}

.nota {
  padding: 12px;
  margin-top: 12px;
  border-radius: 8px;
}

.verde {
  background-color: #173d30;
  color: #55e6a5;
}

.rojo {
  background-color: #482727;
  color: #ff7777;
}

.error {
  color: #ff7777;
}
</style>
