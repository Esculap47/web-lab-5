<template>
  <div class="container">
    <v-row>
      <v-col
        cols="12"
        xs="12"
        sm="6"
        md="4"
        v-for="article in articles"
        :key="article.id"
      >
        <NuxtLink :to="`/news/${article.id}`">
          <NewsCard :article="article" />
        </NuxtLink>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  computed: {
    ...mapGetters({
      articles: "getArticles",
    }),
  },
};
</script>
