<template>
  <v-container>
    <v-row>
      <v-col>
        <v-tabs centered>
          <v-tab> Login </v-tab>
          <v-tab-item class="pa-5">
            <Login></Login>
          </v-tab-item>
          <v-tab> Signup </v-tab>
          <v-tab-item class="pa-5">
            <Signup></Signup>
          </v-tab-item>
        </v-tabs>
      </v-col>
      <v-col>
        <Logout />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Login from "../components/Login.vue";
import Signup from "../components/Signup.vue";
import Logout from "../components/Logout.vue"

export default {
  name: "Home",
  data: () => ({}),
  components: {
    Login,
    Signup,
    Logout
  },
  methods: {
    logout() {
      localStorage.removeItem('token')
      localStorage.removeItem('email')
      localStorage.removeItem('role')
    }
  }
};
</script>
