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
        <input class="form-control" type="text" v-model="newPostsParams.title" />
      </div>
      <div>
        Body:
        <input class="form-control" type="text" v-model="newPostsParams.body" />
        <br />
        <small v-if="newPostsParams.body">{{ 250 - newPostsParams.body.length }} characters remaining</small>
        <br />
      </div>
      <div>
        Image:
        <input class="form-control" type="text" v-model="newPostsParams.image" />
      </div>
      <div>
        <input class="btn btn-primary" type="submit" value="Submit Post" />
      </div>
    </form>
  </div>
</template>

<style scoped></style>
