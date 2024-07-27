<template>
  <div>
    <button @click="$emit('showModal')" class="custom-button">
      Добавить
    </button>

    <table class="custom-table">
      <thead>
        <tr>
          <th>Имя</th>
          <th>Телефон</th>
          <th>Родитель</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ getParentName(user.parentId) }}</td>
          <td>
            <button @click="$emit('deleteUser', user.id)">Удалить</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'TableComponent',
  props: ['users'],
  methods: {
    getParentName(parentId) {
      if (!parentId) return 'Нет';
      const parent = this.users.find(user => user.id === parentId);
      return parent ? parent.name : 'Неизвестно';
    }
  }
};
</script>

<style>
.custom-table {
  width: 100%;
  border-collapse: collapse;
  background-color: white;
  border: 1px solid #ccc;
}

.custom-table th,
.custom-table td {
  padding: 12px;
  border: 1px solid #ccc;
  text-align: left;
}

.custom-table thead {
  background-color: #f2f2f2;
  color: #333;
  font-weight: bold;
}

.custom-table tbody tr:hover {
  background-color: #f5f5f5;
}

.custom-button {
  margin-top: 16px;
  margin-bottom: 16px;
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.custom-button:hover {
  background-color: #0056b3;
}
</style>
