<template>
  <v-app>
    <v-container
      class="d-flex flex-wrap bg-surface-variant mb-6"
      fixed
      fill-height
    >
      <v-row align="center">
        <v-col
          class="mt-6 mb-7 d-flex justify-center"
          v-for="char in characters"
          :key="char.id"
          cols="12"
          md="4"
        >
          <v-card max-width="350" min-height="500" class="d-flex flex-column">
            <v-img
              :src="char.thumbnail.path + '.' + char.thumbnail.extension"
              height="60%"
              width="350"
              max-height="268"
            >
            </v-img>

            <v-row>
              <v-col cols="12" md="12">
                <v-card-title> {{ char.name }} </v-card-title>
                <v-card-text>
                  <v-divider></v-divider>
                  <br />
                  Comics: {{ char.comics.available }}
                  <br />
                  Series: {{ char.series.available }}
                  <br />
                  Stories: {{ char.stories.available }}
                  <br />
                  Events: {{ char.events.available }}
                </v-card-text>
              </v-col>
            </v-row>

            <v-expand-transition>
              <div v-show="char.id === selected">
                <v-divider></v-divider>

                <v-card-text v-if="char.description !== ''" class="wrap-text">
                  {{ char.description }}
                </v-card-text>
                <v-card-text v-else>
                  {{ descNotFound }}
                </v-card-text>
              </div>
            </v-expand-transition>

            <v-card-actions>
              <v-col>
                <v-btn
                  color="#EE171F"
                  @click="
                    $router.push({ name: 'character', params: { id: char.id } })
                  "
                >
                  Explore
                </v-btn>
              </v-col>

              <v-col class="d-flex justify-end">
                <v-btn icon outlined>
                  <v-icon
                    v-model="char.selected"
                    v-if="selected === null && selected != char.id"
                    @click="selected = char.id"
                    >mdi-chevron-down</v-icon
                  >
                  <v-icon v-else @click="selected = null"
                    >mdi-chevron-up</v-icon
                  >
                </v-btn>
              </v-col>
            </v-card-actions>
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
      like: false,
      index: -1,
      props: ['id'],
      descNotFound: 'There is no description provided for this character',
    }
  },
  created() {
    let url =
      'http://gateway.marvel.com/v1/public/characters?ts=7&limit=100&&apikey=7e09e88ea35fdcfd907fc60e66efb209&hash=2556b952565b6bd248a714ffc4786cee'
    axios
      .get(url)
      .then((response) => (this.characters = response.data.data.results))
  },
  methods: {
    goToChar() {},
  },
}
</script>
<style>
.v-card__title {
  font-family: 'Bebas Neue' !important;
}
.v-card__subtitle {
  font-family: 'Bebas Neue' !important;
}
</style>
