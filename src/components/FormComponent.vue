<template>
  <form @submit.prevent="submitForm">

    <div>
      <p>Добавление пользователя </p>
    </div>

    <div>
      <label for="name">Имя:</label>
      <input type="text" id="name" v-model="formData.name" required />
    </div>
    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" v-model="formData.email" required />
    </div>
    <div>
      <label for="parent">Родитель:</label>
      <select id="parent" v-model="formData.parentId">
        <option value="">Без родителя</option>
        <option v-for="user in users" :key="user.id" :value="user.id">
          {{ user.name }}
        </option>
      </select>
    </div>
    <button type="submit">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'FormComponent',
  props: ['users'],
  data() {
    return {
      formData: {
        name: '',
        email: '',
        parentId: ''
      }
    };
  },
  methods: {
    submitForm() {
      this.$emit('submitForm', this.formData);
      this.formData = { name: '', email: '', parentId: '' };
    }
  }
};
</script>

<style scoped>
form {
  max-width: 450px;
  margin: 20px auto;
  padding: 25px;
  background-color: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

p {
  font-size: 1.4em;
  color: #2c3e50;
  text-align: center;
  margin-bottom: 25px;
  font-weight: 600;
}

div {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  color: #34495e;
}

input[type="text"],
input[type="email"] {
  max-width: 50%;
  padding: 12px;
  border: 2px solid #bdc3c7;
  border-radius: 6px;
  font-size: 16px;
  transition: border-color 0.3s ease;
}

input[type="text"]:focus,
input[type="email"]:focus {
  border-color: #3498db;
  outline: none;
}

button {
  width: 100%;
  padding: 12px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 6px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #2980b9;
}
</style>

