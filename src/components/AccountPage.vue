<template>
  <div class="account-page">
    <h2>Аккаунт</h2>

    <!-- Кнопка "Назад" -->
    <button @click="goBack" class="back-button">Назад</button>


    <div v-if="user">
      <p>Никнейм: {{ user.nickname }} <button @click="editField('nickname')">edit</button></p>
      <p>Почта: {{ user.email }} <button @click="editField('email')">edit</button></p>
      <p>Пароль: ******** <button @click="editField('password')">edit</button></p>

      <div v-if="editingField">
        <input type="text" v-model="newValue" />
        <button @click="saveChanges">Сохранить</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: null,
      editingField: null,
      newValue: ''
    };
  },
  methods: {
    goBack() {
      // Возвращает пользователя на предыдущую страницу
      window.history.back();
    },
    editField(field) {
      this.editingField = field;
      this.newValue = this.user[field];
    },
    saveChanges() {
      this.user[this.editingField] = this.newValue;
      localStorage.setItem('userData', JSON.stringify(this.user));
      this.editingField = null;
    }
  },
  mounted() {
    const user = JSON.parse(localStorage.getItem('userData'));
    if (user) {
      this.user = user;
    }
  }
}
</script>

<style scoped>
.account-page {
  padding: 20px;
  max-width: 600px;
  margin: 0 auto;
  background-color: #f0f4f8;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  font-family: 'Arial', sans-serif;
}

h2 {
  color: #333;
  text-align: center;
  font-size: 28px;
  margin-bottom: 20px;
}

p {
  font-size: 18px;
  color: #555;
  margin: 10px 0;
}

button {
  cursor: pointer;
  border: none;
  border-radius: 8px;
  padding: 8px 15px;
  font-size: 16px;
  transition: background-color 0.3s, transform 0.3s;
}

button:hover {
  background-color: #0056b3;
  color: white;
  transform: scale(1.05);
}

.back-button {
  display: inline-block;
  background-color: #007bff;
  color: white;
  padding: 12px 20px;
  margin-bottom: 20px;
  font-size: 16px;
  border-radius: 8px;
  text-align: center;
  transition: background-color 0.3s ease, box-shadow 0.3s ease;
}

.back-button:hover {
  background-color: #0062cc;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  width: 100%;
  margin: 10px 0;
  font-size: 16px;
}

input:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}
</style>
