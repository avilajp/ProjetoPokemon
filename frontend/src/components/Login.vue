<template>
  <div class="container">
    <div class="form-container">
      <h2>Login</h2>
      <form @submit.prevent="login">
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="email" required />
        </div>
        <div>
          <label for="password">Senha:</label>
          <input type="password" id="password" v-model="password" required />
        </div>
        <button type="submit">Entrar</button>
        <button type="button" class="register-button" @click="goToRegister">Registrar</button>
        <div v-if="errorMessage" class="error">{{ errorMessage }}</div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      email: '',
      password: '',
      errorMessage: ''
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post('http://localhost:8000/token', new URLSearchParams({
          username: this.email,
          password: this.password
        }), {
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
          }
        });
        const { access_token } = response.data;
        localStorage.setItem('token', access_token);
        this.$router.push('/home');
      } catch (error) {
        if (error.response) {
          console.log('Erro no login:', error.response);
          this.errorMessage = 'Erro no login: ' + (error.response.data.detail || 'Erro desconhecido');
        } else {
          this.errorMessage = 'Erro desconhecido';
        }
      }
    },
    goToRegister() {
      this.$router.push('/register');
    }
  }
};
</script>

<style scoped>
h2 {
  text-align: left;
}

form div {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #666;
  background-color: #222;
  color: white;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #555;
  border: none;
  border-radius: 4px;
  color: white;
  font-size: 16px;
}

button:hover {
  background-color: #666;
}

.register-button {
  background: none;
  color: #888;
  border: none;
  cursor: pointer;
  font-size: 14px;
  margin-top: 10px;
}

.register-button:hover {
  text-decoration: underline;
}

.error {
  color: red;
  margin-top: 10px;
}
</style>
