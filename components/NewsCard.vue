<template>
  <v-card height="380">
    <v-img
      :src="`/${article.preview_image}`"
      class="white--text align-end"
      gradient="to top, rgba(0,0,0,.7), rgba(0,0,0,.4)"
      height="250px"
    >
      <v-card-title>
        {{ article.name }}
        <v-spacer />
        <span class="font-weight-light">{{ article.date }}</span>
      </v-card-title>
    </v-img>

    <v-card-text>
      <p>{{ article.shortDesc }}</p>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: ["article"],
};
</script>

<style lang="scss" scoped>
</style>
