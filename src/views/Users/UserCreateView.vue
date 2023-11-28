<script>
import axios from "axios";

export default {
  name: "UserCreateView",
  data() {
    return {
      model: {
        userDetail: {
          firstName: '',
          lastName: '',
          age: '',
          birthday: '',
          userId: ''
        }
      }
    }
  },
  methods: {
    saveUser() {
      axios.post('http://localhost:8080/userDetail', this.model.userDetail)
          .then(res => {
            alert('Student was saved successful');
            this.model.userdetail = {
              firstName: '',
              lastName: '',
              age: '',
              birthday: '',
              userId: ''
            }
          }).catch(function (error) {
        // hangle error on UI site
      })
    }
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header">
        <h4>Add Students</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">First Name</label>
          <input type="text" v-model="model.userDetail.firstName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.userDetail.lastName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.userDetail.age" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Birthday</label>
          <input type="text" v-model="model.userDetail.birthday" class="form-control">
        </div>
        <div class="mb-3">
          <button type="button" @click="saveUser" class="btn btn-primary">
            Save
          </button>&nbsp;
          <RouterLink to="/userDetail" class="btn btn-primary">
            Back
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>