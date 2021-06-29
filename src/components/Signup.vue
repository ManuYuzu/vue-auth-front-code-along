<template>
  <div class="d-flex justify-center">
    <v-snackbar dark v-model="snackbar" top right text>
      <p class="text-center ma-0">Signup Successful!</p>
    </v-snackbar>
    <v-card width="500px">
      <v-card-title>Signup </v-card-title>
      <v-card-text>
        <v-text-field
          ref="name"
          type="text"
          label="Name"
          v-model="name"
        ></v-text-field>
        <v-text-field
          ref="email"
          type="text"
          label="Email"
          v-model="email"
          :rules="[rules.email]"
        ></v-text-field>
        <v-text-field
          ref="password"
          type="password"
          label="Password"
          v-model="password"
        ></v-text-field>
        <v-text-field
          type="password"
          label="Repeat Password"
          v-model="confPass"
          :rules="[confPassRule]"
        ></v-text-field>
        <v-select
          label
          :items="['user', 'master', 'admin']"
          placeholder="Select a role"
          v-model="role"
          outlined
        ></v-select>
      </v-card-text>

      <v-divider></v-divider>

      <v-card-actions>
        <v-btn color="success" @click.prevent="submit">Signup</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import authService from "@/sevices/authService"

export default {
  name: "HelloWorld",

  data: () => ({
    name: "",
    email: "",
    password: "",
    confPass: "",
    role: "",
    formHasErrors: false,
    snackbar: false,
    rules: {
      email: (value) =>
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(
          value
        ) || "Email doesn't have the right format",
      // password: (value) =>
      //   /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])[0-9a-zA-Z]{8,}$/.test(value) ||
      //   "8 characters, lowercase and uppercase",
    },
  }),
  computed: {
    confPassRule() {
      return () => this.password === this.confPass || "Passwords do not match";
    },
    form() {
      return {
        email: this.email,
        password: this.password,
      };
    },
  },
  methods: {
    submit() {
      this.formHasErrors = false;

      Object.keys(this.form).forEach((field) => {
        if (!this.form[field]) this.formHasErrors = true;

        this.$refs[field].validate(true);
      });

      if (!this.formHasErrors) this.signup();
    },
    signup() {
      authService
        .signup(this.name, this.email, this.password, this.role)
        .then(response => {
          localStorage.setItem('token', response.token)
          localStorage.setItem('email', response.role)
          localStorage.setItem('role', response.email)

        })
        .catch(err => { console.log(err) })
    }
  },
};
</script>
