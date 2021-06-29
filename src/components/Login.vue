<template>
  <div class="d-flex justify-center">
    <v-snackbar dark v-model="snackbar" top right text>
      <p class="text-center ma-0">{{ snackText }}</p>
    </v-snackbar>
    <v-card width="500px">
      <v-card-title> Login </v-card-title>
      <v-card-text>
        <v-text-field type="text" label="Email" v-model="email"></v-text-field>
        <v-text-field
          type="password"
          label="Password"
          v-model="password"
        ></v-text-field>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-btn color="success" @click="login">Login</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>

import authService from "@/sevices/authService"

export default {
  name: "HelloWorld",

  data: () => ({
    email: "",
    password: "",
    snackbar: false,
    snackText: "",
  }),
  methods: {
    login() {
      authService
        .login(this.email, this.password)
        .then(response => {
          if (response.token) {
            localStorage.setItem('token', response.token)
            localStorage.setItem('email', response.role)
            localStorage.setItem('role', response.email)
            this.$router.push("/logged")
          }
        })
        .catch(err => console.log(err))
    }
  }
};
</script>
