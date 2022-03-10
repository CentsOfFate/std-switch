<template>
  <v-app>
    <v-main>
      <AppBar />
      <GetProducts/>
    </v-main>
  </v-app>
</template>

<script>
import GetProducts from './components/GetProducts.vue'
import AppBar from './components/AppBar.vue'

export default {
  name: 'App',

  components: {
    GetProducts,
    AppBar
},

  data: () => ({
    //
  }),
}
</script>
