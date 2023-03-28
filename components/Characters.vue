<template>
  <v-app>
    <div class="d-flex flex-wrap bg-surface-variant justify-space-between mb-6" >
      <div class="mt-2 mb-8 mx-10 ma-2" v-for="char in characters" :key="char.id">
        <v-card  max-width="344" height="100%">
          <v-img :src="char.thumbnail.path + '.'+ char.thumbnail.extension" height="60%"> </v-img>

          <v-card-title> {{ char.name }} </v-card-title>

          <v-card-subtitle> Comics: {{ char.comics.available }} </v-card-subtitle>

          <v-card-actions>
            <v-btn color=red bottom absolute> Explore </v-btn>

            <v-spacer></v-spacer>

            <v-btn icon outlined bottom right absolute>
              <v-icon v-if="selected === null" @click="selected = char.id">mdi-chevron-down</v-icon>
              <v-icon v-else @click="selected = null">mdi-chevron-up</v-icon>
            </v-btn>
          </v-card-actions>

          <v-expand-transition>
            <div v-show="char.id === selected">
              <v-divider></v-divider>

              <v-card-text>
                {{ char.description }}
              </v-card-text>
            </div>
          </v-expand-transition>
        </v-card>
      </div>
    </div>
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
