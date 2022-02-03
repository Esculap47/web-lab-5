<template>
  <div>
    <v-img
      :src="`/${article.full_image}`"
      class="white--text align-end mb-10"
      gradient="to top, rgba(0,0,0,.7), rgba(0,0,0,.5)"
      height="200px"
    >
      <v-card-title class="font-weight-medium">
        <h3 class="display-3 mr-5">{{ article.name }}</h3>
        <span class="date">{{ article.date }}</span>
      </v-card-title>
    </v-img>

    <p class="ma-5 text-justify">{{ article.desc }}</p>

    <div class="wrapper ma-5">
      <h3 class="display-5 text-center">Написать комментарий</h3>

      <form @submit.prevent="handleForm" class="mb-5 d-flex gap-5">
        <v-text-field
          v-model="name"
          label="Никнейм"
          required
          class="mr-10"
        ></v-text-field>

        <v-text-field
          v-model="comment"
          label="Комментарий"
          required
          class="mr-10"
        ></v-text-field>

        <v-btn class="mr-4" type="submit">Отправить</v-btn>
      </form>

      <h3 class="title text-center">Комментарии ({{ comments.length }})</h3>

      <v-list class="comments">
        <v-list-item
          v-for="comment in comments"
          :key="comment.title"
          class="comment mb-5"
        >
          <v-list-item-content>
            <v-list-item-title>{{ comment.user_name }}</v-list-item-title>
            <v-list-item-subtitle>{{ comment.comment }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
  data: () => ({
    name: "",
    comment: "",
  }),
  methods: {
    async handleForm() {
      try {
        const user_name = this.name,
          comment = this.comment;
        await fetch(
          `http://demo-api.vsdev.space/api/articles/${this.article.id}/comments`,
          {
            method: "POST",
            body: JSON.stringify({ user_name, comment }),
          }
        );
        this.$store.dispatch("activeArticle/fetchComments", this.article.id);
        this.name = "";
        this.comment = "";
      } catch (e) {
        console.log(e);
      }
    },
  },
  computed: {
    ...mapGetters({
      comments: "activeArticle/getComments",
      article: "activeArticle/getArticle",
    }),
  },
  mounted() {
    this.$store.dispatch("activeArticle/initArticle", this.$route.params.id);
  },
};
</script>

<style scoped>
.comments {
    background-color: transparent;
}

.comment {
    border-bottom: 1px solid #464646;
}
</style>