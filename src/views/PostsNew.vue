<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostsParams: {},
      errors: [],
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts.json", this.newPostsParams)
        .then((response) => {
          console.log("Success!", response.data);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div>
    <h1>New Post</h1>
    <form v-on:submit.prevent="createPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div>
        Title:
        <input type="text" v-model="newPostsParams.title" />
      </div>
      <div>
        Body:
        <input type="text" v-model="newPostsParams.body" />
      </div>
      <div>
        Image:
        <input type="text" v-model="newPostsParams.image" />
      </div>
      <div>
        <input type="submit" value="Submit Post" />
      </div>
    </form>
  </div>
</template>
