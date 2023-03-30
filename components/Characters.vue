<template>
  <v-app>
    
      <v-container
        class="d-flex flex-wrap bg-surface-variant mb-6" fluid fill-height
      >
      <v-row justify="center">
        <v-col
          class="mt-6 mb-7"
          v-for="char in characters"
          :key="char.id"
          cols="12"
          md="4"
        >
          <v-card max-width="350" height="100%" class="d-flex flex-column">
            <v-img
              :src="char.thumbnail.path + '.' + char.thumbnail.extension"
              height="60%"
              width="350"
            >
            </v-img>

            <v-row>
              <v-col cols="12" md="12">
                <v-card-title> {{ char.name }} </v-card-title>

                <v-card-subtitle>
                  Comics: {{ char.comics.available }}
                </v-card-subtitle>
              </v-col>
            </v-row>

            <v-expand-transition>
              <div v-show="char.id === selected">
                <v-divider></v-divider>

                <v-card-text class="wrap-text">
                  {{ char.description }}
                </v-card-text>
              </div>
            </v-expand-transition>
            <v-row>
              <v-card-actions>
                <v-col>
                  <v-btn color="#EE171F"> Explore </v-btn>
                </v-col>
                <v-spacer></v-spacer>
                <v-col>
                  <v-btn icon outlined>
                    <v-icon v-if="selected === null" @click="selected = char.id"
                      >mdi-chevron-down</v-icon
                    >
                    <v-icon v-else @click="selected = null"
                      >mdi-chevron-up</v-icon
                    >
                  </v-btn>
                </v-col>
              </v-card-actions>
            </v-row>
          </v-card>
        </v-col>
        </v-row>
      </v-container>
    
  </v-app>
</template>
<script>
import axios from 'axios'

export default {
  name: 'Characters',

  data() {
    return {
      characters: [],
      selected: null,
    }
  },
  created() {
    let url =
      'http://gateway.marvel.com/v1/public/characters?ts=7&limit=100&&apikey=7e09e88ea35fdcfd907fc60e66efb209&hash=2556b952565b6bd248a714ffc4786cee'

    axios
      .get(url)
      .then((response) => (this.characters = response.data.data.results))
  },
}
</script>
<style>
.v-card__title {
  font-family: 'Bebas Neue';
}
.v-card__subtitle {
  font-family: 'Bebas Neue';
}
</style>
