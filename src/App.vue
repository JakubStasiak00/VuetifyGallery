<template>
  <v-app>
    <v-toolbar :elevation="4" class="v-theme--dark bg-indigo-lighten-1">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Vuetify Gallery</v-toolbar-title>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" temporary>

    </v-navigation-drawer>

    <v-container>
      <v-row no-gutters>
        <v-col v-for="n in 12">
          <v-img v-for="image in images" :key="image.id" :src="image.url" class=""></v-img>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script setup>
import { computed, onBeforeMount, ref } from 'vue';

const drawer = ref(false)
const images = ref([])

const getImages = async () => {
  fetch("https://jsonplaceholder.typicode.com/photos?_limit=100")
  .then(response => response.json())
  .then(res => {
    images.value = res
  })
  .catch(err => {
    console.log(err)
  })
}

onBeforeMount(() => {
  getImages()
})

</script>
