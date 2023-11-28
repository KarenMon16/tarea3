<script>
import axios from "axios";

export default {
  name: "UserEditView",
  data() {
    return {
      id: '',
      model: {
        user: {
          firstName: '',
          lastName: '',
          age: '',
          birthday:'',
          userId: '',
        }
      }
    }
  },
  methods: {
    get(id) {
      axios.get(`http://localhost:8080/userDetails/${id}`).then(res => {
        this.model.user = res.data;
      }).catch(function (error) {
        // handle error on UI site
      })
    },
    update() {
      axios.put(`http://localhost:8080/userDetails//${this.id}`, this.model.user)
          .then(res => {
            alert('Se edito los datos detallados del usuario');
          }).catch(function (error) {
        // handle error on UI site
      })
    }
  },
  mounted() {
    this.id = this.$route.params.get;
    this.get(this.id);
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Edit Student</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">First Name</label>
          <input type="text" v-model="model.user.firstName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.user.lastName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.user.age" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.user.birthday" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Card Number</label>
          <input type="text" v-model="model.user.userId" class="form-control">
        </div>
        <div class="mb-3">
          <button type="button" @click="update" class="btn btn-primary">
            Edit
          </button>&nbsp;
          <RouterLink to="/users" class="btn btn-primary">
            Back
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>