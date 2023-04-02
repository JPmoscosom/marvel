<template>
    <v-app-bar color="teal-darken-4" image="https://e0.pxfuel.com/wallpapers/1008/153/desktop-wallpaper-marvel-comics-comic-book-marvel-comics-marvel-black-and-white-comic.jpg">
      <template v-slot:prepend>
        <v-app-bar-nav-icon></v-app-bar-nav-icon>
      </template>
      <v-img
        class="ml-10"
        src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/Marvel_Logo.svg/1200px-Marvel_Logo.svg.png"
        max-height="60"
        max-width="60"
        contain
      ></v-img>

      <v-app-bar-title class="ml-6">{{ title }}</v-app-bar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-heart</v-icon>
      </v-btn>

      <v-btn icon class="mr-10">
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>
</template>
<script>
export default {
  data() {
    return {
      title: 'CHARACTERS',
    }
  },
}
</script>

<style>
.v-app-bar-title__content {
  width: 200px !important;
  font-family: 'Bebas Neue';
}
</style>
