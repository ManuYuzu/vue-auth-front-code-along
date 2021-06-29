<template>
  <div>
    <v-btn color="red" dark @click="logout">
      Logout
    </v-btn>
  </div>
</template>

<script>
  export default {
    name: "Logout",
    methods: {
      logout() {
        localStorage.removeItem('token')
        localStorage.removeItem('email')
        localStorage.removeItem('role')
        this.$router.push("/")
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>