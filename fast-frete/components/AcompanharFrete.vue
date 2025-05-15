<template>
   <div class="bg-white p-6 rounded shadow-md max-w-xl mx-auto">
    <h2 class="text-xl font-semibold mb-4">Acompanhar Frete</h2>

    <form @submit.prevent="buscarStatus">
      <label for="codigo" class="block mb-2 font-medium">Código de Rastreamento</label>
      <input
        id="codigo"
        v-model="codigo"
        type="text"
        placeholder="Ex: FF123456BR"
        class="w-full border border-gray-300 rounded px-4 py-2 mb-4"
      />

      <button
        type="submit"
        class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700"
      >
        Buscar
      </button>
    </form>

    <div v-if="status" class="mt-6 p-4 border rounded bg-gray-100">
      <p class="font-medium">Status Atual:</p>
      <p class="text-lg text-blue-700">{{ status }}</p>
    </div>
  </div>
  
</template>

<script setup>
import { ref } from 'vue'

const codigo = ref('')
const statusFrete = ref(null)

function buscarStatus() {
  // Simulação de status
  if (codigo.value.trim() !== '') {
    statusFrete.value = {
      status: 'Em trânsito',
      local: 'Centro de Distribuição - Curitiba'
    }
  }
}
</script>

<style scoped>
.input {
  display: block;
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 0.375rem;
}

.btn-primary {
  background-color: #2563eb;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 0.375rem;
}
</style>
