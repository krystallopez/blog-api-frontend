<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "All Posts",
      posts: [],
      currentPost: {},
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
    <div class="row">
      <div class="col-sm-4" v-for="post in posts" v-bind:key="post.id" v-on:mouseover="currentPost = post">
        <div class="card mb-4" v-bind:class="{ selected: post == currentPost }">
          <img class="m-auto card-img-top" v-bind:src="post.image" v-bind:alt="post.title" />
          <div class="card-body">
            <h5 class="card-title">{{ post.title }}</h5>
            <p class="card-text">{{ post.body }}</p>
            <a v-bind:href="`/posts/${post.id}`" class="btn btn-dark">To Post</a>
          </div>
        </div>
      </div>
    </div>
    <!-- <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.title }}</h2>
      <img v-bind:src="post.image" v-bind:alt="post.title" />
      <h3>{{ post.body }}</h3>
      <a v-bind:href="`/posts/${post.id}`">To Post</a>
    </div> -->
  </div>
</template>

<style scoped>
.card img {
  object-fit: cover;
  height: 250px;
}
.selected {
  background-color: cyan;
  transition: background-color 1s ease;
}
</style>
