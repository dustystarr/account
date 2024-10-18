<template>
    <div v-if="showRegistrationForm" class="registration-modal">
      <form @submit.prevent="register">
        <label for="nickname">Никнейм:</label>
        <input type="text" v-model="nickname" required />

        <label for="email">Почта:</label>
        <input type="email" v-model="email" required />

        <label for="password">Пароль:</label>
        <input type="password" v-model="password" required />

        <label for="confirmPassword">Подтверждение пароля:</label>
        <input type="password" v-model="confirmPassword" required />

        <button type="submit" class="submit-button">Зарегистрироваться</button>
      </form>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        nickname: '',
        email: '',
        password: '',
        confirmPassword: '',
        showRegistrationForm: true
      };
    },
    methods: {
      register() {
        if (this.password === this.confirmPassword) {
          const userData = {
            nickname: this.nickname,
            email: this.email,
            password: this.password
          };
          localStorage.setItem('userData', JSON.stringify(userData));
          this.showRegistrationForm = false;
          this.$router.push('/products');
        } else {
          alert('Пароли не совпадают!');
        }
      }
    },
    mounted() {
      const user = localStorage.getItem('userData');
      if (user) {
        this.$router.push('/products');
      }
    }
  }
  </script>

  <style scoped>
  .registration-modal {
    background-color: #f0f4f8;
    padding: 30px;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    max-width: 600px;
    margin: 50px auto;
    font-family: 'Arial', sans-serif;
  }

  .registration-modal form {
    display: flex;
    flex-direction: column;
  }

  .registration-modal label {
    margin-bottom: 8px;
    font-weight: bold;
    font-size: 16px;
    color: #333;
  }

  .registration-modal input {
    padding: 12px;
    margin-bottom: 20px;
    border: 1px solid #ccc;
    border-radius: 6px;
    font-size: 16px;
    transition: border-color 0.3s, box-shadow 0.3s;
  }

  .registration-modal input:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
  }

  button {
    background-color: #007bff;
    color: white;
    padding: 12px;
    border: none;
    cursor: pointer;
    border-radius: 8px;
    font-size: 16px;
    transition: background-color 0.3s ease, transform 0.3s;
  }

  button:hover {
    background-color: #0056b3;
    transform: scale(1.05);
  }
  </style>
