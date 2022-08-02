<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "All Posts",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts: function () {
      axios.get("/posts.json").then((response) => {
        this.posts = response.data;
        console.log("All Posts", response.data);
      });
    },
  },
};
</script>

<template>
  <div>
    <h1>All Posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.title }}</h2>
      <img v-bind:src="post.image" v-bind:alt="post.title" />
      <h3>{{ post.body }}</h3>
      <a v-bind:href="`/posts/${post.id}`">To Post</a>
    </div>
  </div>
</template>

<style scoped></style>
