<template>
  <div>
    <h1>Get single post</h1>
    <div v-if="posts">
      {{ posts }}
    </div>
    <div v-if="$apollo.loading"><h1>LOADING</h1></div>
    <div v-if="error">Error: {{ error }}</div>
  </div>
</template>

<script>
// @ is an alias to /src
import { GET_SINGLE_POST_QUERY } from "@/queries/getPosts";
export default {
  name: "Home",
  components: {},
  data() {
    return {
      posts: null,
      error: null
    };
  },
  mounted() {
    console.log(this.$apollo);
  },
  apollo: {
    posts: {
      query: GET_SINGLE_POST_QUERY,
      variables() {
        return {
          slug: "test-post-two"
        };
      },
      error(error) {
        this.error = JSON.stringify(error.message);
      },
      result(ApolloQueryResult) {
        // console.log(ApolloQueryResult.data);
        // console.log(ApolloQueryResult.data.posts.length);
        if (!ApolloQueryResult.data.posts.length) {
          // eslint-disable-next-line no-unused-vars
          this.$router.push("/404").catch(err => {
            console.log(err);
          });
        }
      }
    }
  }
};
</script>
