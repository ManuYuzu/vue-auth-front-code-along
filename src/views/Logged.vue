<template>
  <div>
    <v-app-bar>
      <v-row justify="center">
        <v-col cols="2" justify="center">
          <v-btn>Types</v-btn>
        </v-col>
        <v-col cols="2" justify="center">
          <v-btn>Pokemon</v-btn>
        </v-col>
        <v-col cols="2" justify="center">
          <Logout />
        </v-col>
      </v-row>

    </v-app-bar>
  </div>
</template>

<script>
import Logout from "@/components/Logout.vue"

  export default {
    name: "Logged",
    components: {
      Logout,
    }
  }
</script>

<style lang="scss" scoped>

</style>