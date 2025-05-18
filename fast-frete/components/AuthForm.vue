<!-- components/AuthForm.vue -->
<template>
  <div class="w-full max-w-md p-6 bg-white rounded-2xl shadow-lg">
    <h2 class="text-2xl font-bold text-center mb-4">
      {{ isLogin ? 'Entrar na conta' : 'Criar nova conta' }}
    </h2>

    <form @submit.prevent="handleSubmit" class="space-y-4">
      <div v-if="!isLogin">
        <label class="block text-sm font-medium text-gray-700">Nome</label>
        <input v-model="form.nome" type="text" class="input p-1" placeholder="Seu nome" />
      </div>

      <div>
        <label class="block text-sm font-medium text-gray-700">Email</label>
        <input v-model="form.email" type="email" class="input p-1" placeholder="seu@email.com" />
      </div>

      <div>
        <label class="block text-sm font-medium text-gray-700">Senha</label>
        <input v-model="form.senha" type="password" class="input p-1" placeholder="Sua senha" />
      </div>

      <button type="submit" class="w-full py-2 px-4 bg-blue-600 hover:bg-blue-700 text-white font-semibold rounded-lg transition">
        {{ isLogin ? 'Entrar' : 'Registrar' }}
      </button>
    </form>

    <div class="text-center mt-4">
      <p class="text-sm">
        {{ isLogin ? 'Não tem conta?' : 'Já tem uma conta?' }}
        <button @click="isLogin = !isLogin" class="text-blue-600 hover:underline ml-1">
          {{ isLogin ? 'Cadastre-se' : 'Entrar' }}
        </button>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const isLogin = ref(true)

const form = ref({
  nome: '',
  email: '',
  senha: ''
})

function handleSubmit() {
  if (isLogin.value) {
    console.log('Login:', form.value)
    // Aqui vai o fetch/login
  } else {
    console.log('Registro:', form.value)
    // Aqui vai o fetch/registro
  }
}
</script>

<style scoped>
.input {
  @apply w-full border focus:outline-none ;
}
</style>
