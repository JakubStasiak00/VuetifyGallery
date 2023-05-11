<template>
  <v-app>
    <v-toolbar :elevation="4" class="v-theme--dark bg-indigo-lighten-1">
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title @click="debug">Vuetify Gallery</v-toolbar-title>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" temporary>

    </v-navigation-drawer>

    <v-container>
      <v-row no-gutters>
        <v-col v-for="n in 100" :key="n" cols="2">
          <v-card>
            <v-img :src="images[n - 1]" aspect-ratio="1" class=""></v-img>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script setup>
import { computed, onBeforeMount, ref } from 'vue';

const drawer = ref(false)
const images = ref([])

const debug = () => {
  console.log(images.value)
}

const getImages = async () => {
  fetch("https://jsonplaceholder.typicode.com/photos?_limit=100", { timeout: 10000 })
    .then(response => response.json())
    .then(res => {
      res.forEach(img => {
        images.value.push(img.url)
      })
    })
    .catch(err => {
      console.log(err)
    })
}

onBeforeMount(() => {
  getImages()
})

</script>
