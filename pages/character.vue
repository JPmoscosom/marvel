<template>
  <v-app>
    <Appbar />
    <v-container v-for="char in character" :key="char.id" fluid fill-height>
      <v-row>
        <v-card class="d-flex elevation-5 my-6 mx-5" width="100%">
          <v-col cols="12" md="4">
            <v-img
              class="rounded"
              :src="char.thumbnail.path + '.' + char.thumbnail.extension"
              width="400"
              height="400"
            >
            </v-img>
          </v-col>
          <v-col md="8">
            <v-card-title>
              {{ char.name }}
            </v-card-title>
            <v-divider></v-divider>
            <v-spacer></v-spacer>
            <br />
            <v-card-title> Description </v-card-title>
            <v-card-text v-if="char.description !== ''">
              {{ char.description }}
            </v-card-text>
            <v-card-text v-else>
              {{ descNotFound }}
            </v-card-text>
            <v-card-text>
              <br />
              <v-divider></v-divider>
              <br />
              Available Comics: {{ char.comics.available }}
              <br />
              Available Series: {{ char.series.available }}
              <br />
              Available Stories: {{ char.stories.available }}
              <br />
              Available Events: {{ char.events.available }}
            </v-card-text>
          </v-col>
        </v-card>
      </v-row>
      <v-row align="center" justify="center">
        
        <v-card class="elevation-5 my-6 mx-5" max-width="95%">
          <v-row align="center" justify="center">
            <v-card-title> COMICS </v-card-title>
          </v-row>
          <v-slide-group center-active show-arrows class="pa-4">
            <v-col cols="12" class="d-flex justify-content-center">
              <v-slide-group-item
                v-for="comic in comics"
                :key="comic.id"
                class="ml-3"
              >
                <v-card
                  max-width="350"
                  height="600"
                  class="d-flex flex-column"
                >
                  <v-img
                    :src="
                      comic.thumbnail.path + '.' + comic.thumbnail.extension
                    "
                    max-height="530"
                    class="elevation-5 rounded"
                    height="80%"
                  >
                  </v-img>
                  <v-row justify="center">
                    <v-card-subtitle>
                      {{ comic.title }}
                    </v-card-subtitle>
                  </v-row>
                </v-card>
              </v-slide-group-item>
            </v-col>
          </v-slide-group>
        </v-card>
    
      </v-row>
      <v-row align="center" justify="center">
        <v-card class="elevation-5 my-6 mx-5" max-width="95%">
          <v-row align="center" justify="center">
            <v-card-title> SERIES </v-card-title>
          </v-row>
          <v-slide-group center-active show-arrows class="pa-4">
            <v-col cols="12" class="d-flex justify-content-center">
              <v-slide-group-item
                v-for="serie in series"
                :key="serie.id"
                class="ml-3"
              >
                <v-card
                  max-width="350"
                  min-height="530"
                  class="d-flex flex-column"
                >
                  <v-img
                    :src="
                      serie.thumbnail.path + '.' + serie.thumbnail.extension
                    "
                    height="425"
                    class="elevation-5 rounded"
                    
                  >
                  </v-img>
                  <v-row justify="center">
                    <v-card-subtitle>
                      {{ serie.title }}
                    </v-card-subtitle>
                  </v-row>
                </v-card>
              </v-slide-group-item>
            </v-col>
          </v-slide-group>
        </v-card>
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
      character: [],
      comics: [],
      series: [],
      descNotFound: 'There is no description provided for this character',
    }
  },
  created() {
    const id = this.$route.params.id
    const URL = 'https://gateway.marvel.com/v1/public/characters/'
    const API =
      '?ts=7&apikey=7e09e88ea35fdcfd907fc60e66efb209&hash=2556b952565b6bd248a714ffc4786cee'
    let url = `${URL}` + `${id}` + `${API}`
    let urlComics = `${URL}` + `${id}` + '/comics' + `${API}`
    let urlSeries = `${URL}` + `${id}` + '/series' + `${API}`

    axios
      .get(url)
      .then((response) => (this.character = response.data.data.results))

    axios
      .get(urlComics)
      .then((response) => (this.comics = response.data.data.results))

    axios
      .get(urlSeries)
      .then((response) => (this.series = response.data.data.results))
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
.v-card__text  {
  font-family: 'Bebas Neue' !important;
}

</style>
