<template>
  <div class="container">
    <div class="form-container">
      <h2>Registro</h2>
      <form @submit.prevent="register">
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="email" required />
          <span v-if="emailError" class="error">{{ emailError }}</span>
        </div>
        <div>
          <label for="password">Senha:</label>
          <input type="password" id="password" v-model="password" required />
        </div>
        <div>
          <label for="confirmPassword">Confirmar Senha:</label>
          <input type="password" id="confirmPassword" v-model="confirmPassword" required />
          <span v-if="passwordError" class="error">{{ passwordError }}</span>
        </div>
        <button type="submit">Registrar</button>
        <div class="link-container">
          <button type="button" @click="goToLogin">Login</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      confirmPassword: '',
      emailError: '',
      passwordError: ''
    };
  },
  methods: {
    async register() {
      this.emailError = '';
      this.passwordError = '';

      if (!this.email || !this.password || !this.confirmPassword) {
        this.passwordError = 'Todos os campos são obrigatórios';
        return;
      }

      if (this.password !== this.confirmPassword) {
        this.passwordError = 'As senhas não coincidem';
        return;
      }

      try {
        const response = await fetch('http://localhost:8000/api/register', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json'
          },
          body: JSON.stringify({
            email: this.email,
            password: this.password
          })
        });

        if (!response.ok) {
          const errorData = await response.json();
          throw new Error(errorData.detail || 'Erro desconhecido');
        }

        alert('Usuário registrado com sucesso!');
        this.$router.push('/login');
      } catch (error) {
        alert('Erro ao registrar o usuário: ' + error.message);
      }
    },
    goToLogin() {
      this.$router.push('/login');
    }
  }
};
</script>

<style scoped>
h2 {
  text-align: center;
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

.error-message {
  color: #f00;
  margin-bottom: 10px;
}
</style>
