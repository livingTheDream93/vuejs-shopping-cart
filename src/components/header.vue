<template>
  <v-toolbar color="teal lighten-1" dark>
    <v-toolbar-side-icon></v-toolbar-side-icon>
    <v-toolbar-title>Books</v-toolbar-title>
    <v-spacer></v-spacer>
    <div class="hidden-sm-and-down">
      
      <router-link to="/login">
        <v-btn flat>Login</v-btn>
      </router-link>
    </div>
  </v-toolbar>
</template>

<script>
export default {
  name:'headercomp'
}
</script>

<style scoped>

</style>