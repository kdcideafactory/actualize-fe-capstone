<template>
  <div class="signup">

    <!-- Projects Section -->
      <section class="projects-section">
        <div class="container">

          <div class="row">

            <form class="col-6 mx-auto text-center" v-on:submit.prevent="submit()">
              <h1>Signup</h1>
              <ul>
                <li class="text-danger" v-for="error in errors">{{ error }}</li>
              </ul>
              <div class="form-group">
                <label>Name:</label> 
                <input type="text" class="form-control" v-model="name">
              </div>
              <div class="form-group">
                <label>Email:</label>
                <input type="email" class="form-control" v-model="email">
              </div>
              <div class="form-group">
                <label>Password:</label>
                <input type="password" class="form-control" v-model="password">
              </div>
              <div class="form-group">
                <label>Password confirmation:</label>
                <input type="password" class="form-control" v-model="passwordConfirmation">
              </div>
              <div class="form-group">
                <label>Address:</label> 
                <input type="text" class="form-control" v-model="address">
              </div>
              <div class="form-group">
                <label>Bio:</label> 
                <input type="text" class="form-control" v-model="bio">
              </div>
              <div class="form-group">
                <label>Avatar:</label> 
                <input type="text" class="form-control" v-model="avatar">
              </div>
              <input type="submit" class="btn btn-warning" value="Submit">
            </form>

          </div>


        </div>
      </section>


    
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      name: "",
      email: "",
      password: "",
      passwordConfirmation: "",
      address: "",
      bio: "",
      avatar: "",
      errors: []
    };
  },
  methods: {
    submit: function() {
      var params = {
        name: this.name,
        email: this.email,
        password: this.password,
        password_confirmation: this.passwordConfirmation,
        address: this.address,
        bio: this.bio,
        avatar: this.avatar
      };
      axios
        .post("/api/users", params)
        .then(response => {
          this.$router.push("/login");
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    }
  }
};
</script>
