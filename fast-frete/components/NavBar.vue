<template>
  <nav
    class="m-3 rounded-4xl bg-[#DDDDDD] text-[#545454] py-4 px-6 flex justify-between items-center"
  >
    <NuxtLink to="/" class="text-xl font-bold hover:text-[#000000]">LOGO</NuxtLink>
    <div class="flex gap-4 items-center">
      <NuxtLink to="/" class="hover:text-[#000000]" active-class="font-bold"
        >Início</NuxtLink
      >
      <NuxtLink to="/sobre" class="hover:text-[#000000]" active-class="font-bold"
        >Sobre</NuxtLink
      >

      <!-- Menu de Conta -->
      <div class="relative">
        <button
          @click="toggleAccountMenu"
          class="flex items-center gap-1 hover:text-[#000000] focus:outline-none"
        >
          <span>{{ user ? "Minha Conta" : "Entrar" }}</span>
          <svg
            class="h-4 w-4"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path
              fill-rule="evenodd"
              d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
              clip-rule="evenodd"
            />
          </svg>
        </button>

        <!-- Dropdown Menu -->
        <div
          v-show="isAccountMenuOpen"
          class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none z-50"
        >
          <template v-if="user">
            <!-- Itens quando logado -->
            <NuxtLink
              to="/conta/dados"
              class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
              @click.native="isAccountMenuOpen = false"
            >
              Meus Dados
            </NuxtLink>
            <NuxtLink
              to="/conta/configuracoes"
              class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
              @click.native="isAccountMenuOpen = false"
            >
              Configurações
            </NuxtLink>
            <div class="border-t border-gray-200"></div>
            <button
              @click="logout"
              class="block w-full text-left px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
            >
              Sair
            </button>
          </template>
          <template v-else>
            <!-- Itens quando não logado -->
            <NuxtLink
              to="/login"
              class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
              @click.native="isAccountMenuOpen = false"
            >
              Login
            </NuxtLink>
            <NuxtLink
              to="/registro"
              class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
              @click.native="isAccountMenuOpen = false"
            >
              Criar Conta
            </NuxtLink>
          </template>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isAccountMenuOpen: false,
      user: null, // Isso verá do estado de autenticação
    };
  },
  mounted() {
    this.checkAuth();
    document.addEventListener("click", this.handleClickOutside);
  },
  beforeDestroy() {
    document.removeEventListener("click", this.handleClickOutside);
  },
  methods: {
    toggleAccountMenu() {
      this.isAccountMenuOpen = !this.isAccountMenuOpen;
    },
    handleClickOutside(event) {
      if (!this.$el.contains(evente.target)) {
        this.isAccountMenuOpen = false;
      }
    },
    async checkAuth() {
      // Implementar verificação de auth aqui
      // Exemplo: this.user = this.$store.state.auth.user
    },
    async logout() {
      // Logout aqui
      // await this.$store.dispatch('auth/logout')
      this.user = null;
      this.isAccountMenuOpen = false;
      this.$router.push("/login");
    },
  },
};
</script>

<style scoped>
.router-link-exact-active {
  font-weight: bold;
  text-decoration: none;
}
</style>
