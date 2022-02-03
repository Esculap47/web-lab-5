<template>
  <v-row justify="center" align="center">
    <v-carousel>
      <v-carousel-item
        v-for="(slide, i) in sliderImages"
        :key="i"
        :src="`/${slide}`"
        reverse-transition="fade-transition"
        transition="fade-transition"
      ></v-carousel-item>
    </v-carousel>

    <h1 class="mt-15">Добро пожаловать на мой новостной сайт!</h1>
  </v-row>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  name: "IndexPage",

  computed: {
    ...mapGetters({ getSliderArticles: "getSliderArticles" }),

    sliderImages() {
      return this.getSliderArticles.map((article) => article.full_image);
    },
  },
};
</script>
