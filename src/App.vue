<template>
   <div id="app">
    <TableComponent :users="users" @showModal="showModal" @deleteUser="deleteUser" />
    <ModalComponent v-if="isModalVisible" @closeModal="closeModal">
      <FormComponent :users="users" @submitForm="handleSubmit" />
    </ModalComponent>
  </div>
</template>

<script>
import TableComponent from './components/TableComponent.vue';
import ModalComponent from './components/ModalComponent.vue';
import FormComponent from './components/FormComponent.vue';

export default {
  name: 'App',
  components: {
    TableComponent,
    ModalComponent,
    FormComponent
  },
  data() {
    return {
      isModalVisible: false,
      users: JSON.parse(localStorage.getItem('users')) || []
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    },
    handleSubmit(formData) {
      const newUser = {
        id: this.users.length > 0 ? Math.max(...this.users.map(u => u.id)) + 1 : 1,
        ...formData,
        parentId: formData.parentId ? parseInt(formData.parentId) : null
      };
      this.users.push(newUser);
      this.saveToLocalStorage();
      this.closeModal();
    },
    saveToLocalStorage() {
      localStorage.setItem('users', JSON.stringify(this.users));
    },
    deleteUser(userId) {
      this.users = this.users.filter(user => user.id !== userId);
    },
    watch: {
    users: {
      handler() {
        this.saveToLocalStorage();
      },
      deep: true
    }
  }
  }

};
</script>


