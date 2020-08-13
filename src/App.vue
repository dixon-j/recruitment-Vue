<template>
  <v-app>
    <Navbar/>
    <v-main>
        <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from './components/Navbar'

export default {
  name: 'App',

  components: {
    Navbar
  }
}
</script>

<style>
/* .theme--light.v-application{
  background-color:#e0e0e0 !important;
} */
</style>
