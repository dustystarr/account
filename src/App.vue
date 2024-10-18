<template>
  <div>
    <header>
      <nav>
        <ul>
          <li @click="goToAccount"><i class="fas fa-user"></i></li>
          <li v-if="userData" @click="logout" class="logout-button">
            <i class="fas fa-sign-out-alt"></i> <!-- Иконка выхода -->
          </li>
        </ul>
      </nav>
    </header>


    <router-view v-if="!showRegistration" />


    <RegistrationForm v-if="showRegistration" @close="closeRegistrationForm" />
  </div>
</template>

<script>
import RegistrationForm from './components/RegistrationForm.vue';

export default {
  data() {
    return {
      showRegistration: !localStorage.getItem('userData'),
      userData: JSON.parse(localStorage.getItem('userData'))
    };
  },
  methods: {
    closeRegistrationForm() {
      this.showRegistration = false;
      localStorage.setItem('userData', JSON.stringify({ registered: true }));
      this.userData = JSON.parse(localStorage.getItem('userData'));

      this.$router.push('/products');
    },
    goToAccount() {
      this.$router.push('/account');
    },
    logout() {
      localStorage.removeItem('userData');
      this.showRegistration = true;
      this.userData = null;
      this.$router.push('/');
    }
  },
  components: {
    RegistrationForm
  }
};
</script>

<style scoped>
nav ul {
  display: flex;
  justify-content: flex-end;
  list-style-type: none;
}

nav ul li {
  margin-left: 20px;
  cursor: pointer;
  display: flex;
  align-items: center; /* Выравниваем элементы по центру */
}

.logout-button {
  color: #ff4c4c; /* Красный цвет для кнопки выхода */
}
</style>
