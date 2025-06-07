<template>
  <div class="container">
    <h1>Lista de Especialistas</h1>

    <table v-if="especialistas.length">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre completo</th>
          <th>Especialidad</th>
          <th>Registro profesional</th>
          <th>Activo</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="e in especialistas" :key="e.id">
          <td>{{ e.id }}</td>
          <td>{{ e.nombre_completo }}</td>
          <td>{{ e.especialidad }}</td>
          <td>{{ e.registro_profesional }}</td>
          <td>{{ e.activo ? 'Sí' : 'No' }}</td>
        </tr>
      </tbody>
    </table>

    <p v-else>Cargando especialistas o no hay datos</p>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

type Especialista = {
  id: number
  nombre_completo: string
  especialidad: string
  registro_profesional: string
  activo: boolean
}

const especialistas = ref<Especialista[]>([])

onMounted(async () => {
  try {
    const res = await fetch('http://localhost:3333/especialistas')
    especialistas.value = await res.json()
  } catch (error) {
    console.error('Error al cargar especialistas:', error)
  }
})
</script>

<style>
.container {
  max-width: 900px;
  margin: auto;
  font-family: Arial, sans-serif;
}
h1 {
  text-align: center;
  margin-bottom: 20px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}
th {
  background-color: #f4f4f4;
}
</style>
