<template>
  <div class="home-container">
    <h1>Olá!</h1>
    <p>Seja bem-vindo à central de Pokemons!</p>
    
    <div class="search-bar">
      <input type="text" placeholder="Encontre seu pokemon" />
    </div>

    <div class="pokemon-image-container">
      <img src="@/assets/pokemons.png" alt="Pokémons" class="pokemon-image"/>
    </div>

    <div class="pagination">
      <button v-for="page in totalPages" :key="page" @click="goToPage(page)">{{ page }}</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      totalPages: 10
    };
  },
  methods: {
    checkAuth() {
      const token = localStorage.getItem('token');
      if (!token) {
        this.$router.push('/login');
      }
    },
    goToPage(page) {
      // lógica para navegação entre as páginas de pokemons
      console.log(`Navegando para a página ${page}`);
    }
  },
  mounted() {
    this.checkAuth();
  }
};
</script>

<style scoped>
.home-container {
  text-align: center;
  color: #fff;
  background-color: #2f2f2f;
  padding: 20px;
}

.search-bar input {
  width: 100%;
  max-width: 400px;
  padding: 10px;
  margin-bottom: 20px;
  border-radius: 10px;
  border: none;
}

.pokemon-image-container {
  display: flex;
  justify-content: center; /* Centraliza horizontalmente */
  align-items: center; /* Centraliza verticalmente */
  margin: 20px 0;
}

.pokemon-image {
  max-width: 100%;
  height: auto;
  border-radius: 10px;
}

.pagination {
  margin-top: 20px;
}

.pagination button {
  background-color: #444;
  border: none;
  color: #fff;
  padding: 10px;
  margin: 0 5px;
  border-radius: 5px;
  cursor: pointer;
}

.pagination button:hover {
  background-color: #666;
}
</style>
