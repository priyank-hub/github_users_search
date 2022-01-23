<template>
  <v-app>
    <div id="app">
      <div class="container">
        <div class="row justify-content-center align-items-center" style="min-height: 100vh">
          <div class="col-12">
            <Card />
          </div>
        </div>
      </div>
    </div>
  </v-app>
</template>

<script>
import Card from './components/Card.vue'

export default {
  name: 'App',
  components: {
    Card
  }
}
</script>

<style>
  #app {
    font-family: 'Dejavu Sans Mono';
  }
</style>

<style>
@font-face {
  font-family: "Dejavu Sans Mono";
  src: local("Dejavu Sans Mono"),
   url(../public/fonts/dejavu-sans-mono/DejaVuSansMono.ttf) format("truetype");
}
</style>
