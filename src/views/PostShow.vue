<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/posts/" + this.$route.params.id + ".json").then((response) => {
        this.post = response.data;
        console.log("One Post", response.data);
      });
    },
  },
};
</script>

<template>
  <div>
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image" v-bind:alt="post.title" />
    <h2>{{ post.body }}</h2>
    <div>
      <a href="/posts">Back to All Posts</a>
    </div>
  </div>
</template>

<style scoped></style>
