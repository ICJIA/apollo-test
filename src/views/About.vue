<template>
  <div>
    <div v-if="error">Error: {{ this.error }}</div>

    <div v-if="posts">
      {{ posts }}
    </div>
  </div>
</template>

<script>
import { GET_ALL_POSTS_QUERY } from "@/queries/getPosts";
export default {
  data() {
    return {
      posts: null,
      error: null
    };
  },
  async mounted() {
    try {
      this.posts = await this.$apollo.query({
        query: GET_ALL_POSTS_QUERY,
        variables: {}
      });
    } catch (e) {
      console.log("error", e);
      this.error = JSON.stringify(e.message);
    }
  }
};
</script>

<style lang="scss" scoped></style>
