<template>
  <div>
    <v-app-bar
    app
    color="primary"
    dark
  >
    <div class="d-flex align-center">
      <v-img
        alt="Vuetify Logo"
        class="shrink mr-2"
        contain
        src="../assets/to-do-list.png"
        transition="scale-transition"
        width="40"
      />
      <h3>
        TO-DO-LIST
      </h3>
    </div>
  </v-app-bar>
  </div>
</template>
<script>
export default {
  name: 'Appbar'
}
</script>
<style>
  
</style>