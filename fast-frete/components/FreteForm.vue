<template>
<div >
  <div class="p-6 max-w-full mx-auto">

 <!-- this block only use on full page -->

  <!-- <h1 class="text-3xl font-bold mb-6 text-center">Serviços de Frete</h1>
    <div class="flex justify-center gap-6 mb-8">
      <button
        @click="abaAtiva = 'solicitar'"
        :class="[
          'px-4 py-2 rounded',
          abaAtiva === 'solicitar'
            ? 'bg-blue-600 text-white'
            : 'bg-gray-200 text-gray-700 hover:bg-gray-300'
        ]"
      >
        Solicitar Frete
      </button>

      <button
        @click="abaAtiva = 'acompanhar'"
        :class="[
          'px-4 py-2 rounded',
          abaAtiva === 'acompanhar'
            ? 'bg-blue-600 text-white'
            : 'bg-gray-200 text-gray-700 hover:bg-gray-300'
        ]"
      >
        Acompanhar Frete
      </button>
    </div>-->
    

    <div v-if="abaAtiva === 'solicitar'">
      <SolicitarFrete />
    </div>
    <div v-else>
      <AcompanharFrete />
    </div>
  </div>
 </div>
</template>

<script setup>
import { ref } from 'vue'
import SolicitarFrete from '~/components/SolicitarFrete.vue'
import AcompanharFrete from '~/components/AcompanharFrete.vue'

const abaAtiva = ref('solicitar')
</script>
