<script>
import axios from "axios";

export default {
  name: "UserEditView",
  data() {
    return {
      users: []
    }
  },
  methods: {
    getUsers() {
      axios.get('http://localhost:8080/users/allUsers').then(res => {
        this.users = res.data;
      }).catch(function (error) {
        // handle error on UI site
      })
    },
  },
  mounted() {
    this.getUsers();
  }


}
</script>

<template>
  <div class="course">
    <div class="card">
      <div class="card-header">
        <h4>
          Users
          <RouterLink to="/users/create" class="btn btn-primary float-end">
            Add User
          </RouterLink>
        </h4>
      </div>
      <div class="card-body">
        <table class="table table-bordered">
          <thead>
          <tr>
            <th>Nro</th>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Age</th>
            <th>Birthday</th>
            <th>Actions</th>
          </tr>
          </thead>
          <tbody v-if="users.length > 0">
          <tr v-for="(user, id) in this.users" :key="id">
            <td>{{ id + 1 }}</td>
            <td>{{ user.firstName }}</td>
            <td>{{ user.lastName }}</td>
            <td>{{ user.age }}</td>
            <td>{{ user.birthday }}</td>
            <td>{{ user.birthday }}</td>
          </tr>
          </tbody>
          <tbody v-else>
          <tr>
            <td colspan="7">No hay usuarios</td>
          </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>