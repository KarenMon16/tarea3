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
      axios.get('http://localhost:8080/userDetail/allUsers').then(res => {
        this.users = res.data;
      }).catch(function (error) {
        // handle error on UI site
      })
    },

    deleteUser(userId) {
      if (confirm('Are you sure, you want to delete this data?')) {
        axios.delete(`http://localhost:8080/userDetail/${userId}`).then(res => {
          this.getUsers();
        }).catch(function (error) {
          // handle error on UI site
        })
      }
    }
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
          <RouterLink to="/userDetail/create" class="btn btn-primary float-end">
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
            <td>{{ new Date(user.birthday).toLocaleDateString() }}</td>
            <td><RouterLink :to="{ path: '/userDetail/' + user.id + '/edit' }" class="btn btn-success">
              Edit
            </RouterLink>
              <button type="button" @click="deleteUser(user.id)" class="btn btn-danger">
                Delete
              </button></td>
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