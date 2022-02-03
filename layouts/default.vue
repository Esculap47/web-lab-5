<template>
  <v-app dark>
    <v-app-bar clipped-left fixed app>
      <v-toolbar-title>Новостной сайт</v-toolbar-title>
    </v-app-bar>

    <v-navigation-drawer permanent app clipped>
      <v-list nav dense>
        <v-list-item link router to="/">
            <v-list-item-icon>
              <v-icon>mdi-home-variant-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title> Главная </v-list-item-title>
        </v-list-item>

        <v-list-item link router to="/news">
            <v-list-item-icon>
              <v-icon>mdi-newspaper-variant-outline</v-icon>
            </v-list-item-icon>
            <v-list-item-title> Новости </v-list-item-title>
        </v-list-item>

        <v-list-item link router to="/gallery">
            <v-list-item-icon>
              <v-icon>mdi-image-multiple</v-icon>
            </v-list-item-icon>
            <v-list-item-title> Галерея </v-list-item-title>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "DefaultLayout",
  data: () => ({
    items: [
      {
        icon: "mdi-apps",
        title: "Welcome",
        to: "/",
      },
      {
        icon: "mdi-chart-bubble",
        title: "Inspire",
        to: "/inspire",
      },
    ],
  }),

  async created() {
    await this.$store.dispatch("fetchArticles");
  },
};
</script>

<style>
a {
  text-decoration: none;
  color: inherit;
}
</style>
