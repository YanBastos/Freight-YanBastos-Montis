<template>

  <div class="max-w-2xl mx-auto p-6 bg-white rounded-2xl shadow-lg">
    <h2 class="text-2xl font-bold mb-4">Solicitar Frete</h2>

    <form @submit.prevent="avancarPedido">
      <!-- Origem -->
      <h3 class="font-semibold mb-2">Endereço de Origem</h3>
      <div class="grid grid-cols-2 gap-4 mb-4">
        <input v-model="origem.cep" type="text" placeholder="CEP" class="input p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
        <input v-model="origem.rua" type="text" placeholder="Rua" class="input  p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
        <input v-model="origem.numero" type="text" placeholder="Número" class="input  p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
        <input v-model="origem.complemento" type="text" placeholder="Complemento (opcional)" class="input  p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
      </div>

      <!-- Destino -->
      <h3 class="font-semibold mb-2">Endereço de Destino</h3>
      <div class="grid grid-cols-2 gap-4 mb-4">
        <input v-model="destino.cep" type="text" placeholder="CEP" class="input p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
        <input v-model="destino.rua" type="text" placeholder="Rua" class="input p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
        <input v-model="destino.numero" type="text" placeholder="Número" class="input p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
        <input v-model="destino.complemento" type="text" placeholder="Complemento (opcional)" class="input p-1 bg-[#E5DE55] outline-0 focus:outline-none" />
      </div>

      <!-- Peso e descrição -->
      <div class="mb-4">
        <input v-model.number="peso" type="number" min="0" step="0.1" placeholder="Peso da carga (kg)" class="input w-full bg-[#E5DE55] p-1" />
      </div>

      <div class="mb-4">
        <textarea
          v-model="descricaoCarga"
          placeholder="Descrição da carga"
          class="input w-full  bg-[#E5DE55]  p-1"
          rows="3"
        ></textarea>
      </div>

      <!-- Tipo de frete -->
      <div class="mb-4">
        <label class="block mb-1 font-semibold">Tipo de Frete:</label>
        <select v-model="tipoFrete" class="input w-full  bg-[#E5DE55]">
          <option value="comum" >Frete Comum</option>
          <option value="mudanca">Mudança</option>
          <option value="expressa">Entrega Expressa</option>
          <option value="agendada">Entrega Agendada</option>
          <option value="economica">Entrega Econômica</option>
        </select>
      </div>

      <!-- Data e horário -->
      <div class="grid grid-cols-2 gap-4 mb-4  bg-[#E5DE55]">
        <input v-model="dataColeta" type="date" class="input" />
        <input v-model="horarioColeta" type="time" class="input" />
      </div>

      <!-- Botão de ação -->
      <button type="submit" class="bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">
        Avançar
      </button>
    </form>

    
    

   </div> 
   
   <!-- Blocos lado a lado
   <div class="max-w-7xl mt-2 p-6 bg-yellow-400 shadow-md rounded-md">
   
    <div v-if="resumo || fretesDisponiveis.length" class="mt-6 grid grid-cols-1 md:grid-cols-2 gap-4">
       Resumo 
      <div class="p-4 bg-gray-100 rounded text-sm leading-relaxed">
        <p><strong>Frete estimado:</strong>
          <span v-if="tipoFrete === 'mudanca'">A confirmar. Entraremos em contato.</span>
          <span v-else>R$ {{ resumo.valor }}</span>
        </p>
        <p><strong>Data Coleta:</strong> {{ resumo.data || '—' }} às {{ resumo.horario || '—' }}</p>
        <p><strong>Tipo:</strong> {{ tipoFrete }}</p>
        <p><strong>Descrição:</strong> {{ descricaoCarga || '—' }}</p>
      </div>

       Fretes disponíveis 
      <div class="p-4 bg-gray-50 rounded text-sm">
        <h4 class="font-semibold mb-2">Fretes disponíveis para agendamento:</h4>
        <ul class="list-disc pl-5 space-y-1">
          <li v-for="(frete, index) in fretesDisponiveis" :key="index">
            {{ frete.data }} às {{ frete.horario }}
          </li>
        </ul>
      </div>
    </div>
  </div>-->
</template>

<script setup>
import { ref } from 'vue'

const origem = ref({ cep: '', rua: '', numero: '', complemento: '' })
const destino = ref({ cep: '', rua: '', numero: '', complemento: '' })
const peso = ref(0)
const tipoFrete = ref('comum')
const descricaoCarga = ref('')
const dataColeta = ref('')
const horarioColeta = ref('')
const resumo = ref(null)
const fretesDisponiveis = ref([])

function avancarPedido() {
  const distanciaSimulada = 120 // km fictício
  const precoPorKm = 0.6
  const precoPorKg = 0.9
  let valor = 0

  if (tipoFrete.value === 'mudanca') {
    resumo.value = {
      valor: null,
      data: dataColeta.value,
      horario: horarioColeta.value,
    }
  } else {
    if (tipoFrete.value === 'comum') {
      valor = (distanciaSimulada * precoPorKm) + (peso.value * precoPorKg)
    } else if (tipoFrete.value === 'expressa') {
      valor = (distanciaSimulada * precoPorKm * 1.5) + (peso.value * precoPorKg * 1.2)
    } else if (tipoFrete.value === 'agendada') {
      valor = (distanciaSimulada * precoPorKm * 0.9) + (peso.value * precoPorKg)
    } else if (tipoFrete.value === 'economica') {
      valor = (distanciaSimulada * precoPorKm * 0.7) + (peso.value * precoPorKg * 0.8)
    }

    resumo.value = {
      valor: valor.toFixed(2),
      data: dataColeta.value,
      horario: horarioColeta.value,
    }
  }

  fretesDisponiveis.value = [
    { data: '2025-05-10', horario: '09:00' },
    { data: '2025-05-10', horario: '13:00' },
    { data: '2025-05-11', horario: '08:30' },
    { data: '2025-05-12', horario: '14:00' },
  ]
}
</script>

<style scoped>
.input {
  @apply border w-full ;
}
</style>
