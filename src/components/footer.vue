<template>
  <v-footer color="#000C1D">
    <v-row
      justify="center"
      no-gutters
    >
      <v-col
        class=" darken-3 py-4 text-center white--text"
        style="background-color:rgba(0,0,0,0.2);"
        cols="12"
      >
        This page reveals that it has no commercial purpose as an exercise project

        {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
      </v-col>
    </v-row>

  </v-footer>
</template>

<script>
export default {
  name: 'main-footer'
}
</script>

<style scoped>

</style>
