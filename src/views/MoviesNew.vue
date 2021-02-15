<template>
  <div class="movies-new">
    <form v-on:submit.prevent="movieNew()">
      <h1>Create New Movie</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title:</label> 
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>year:</label>
        <input type="text" class="form-control" v-model="year">
      </div>
      <div class="form-group">
        <label>plot:</label>
        <input type="text" class="form-control" v-model="plot">
      </div>
      <!-- <div class="form-group">
        <label>User Id:</label>
        <input type="text" class="form-control" v-model="userId">
      </div> -->
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      title: "",
      year: "",
      plot: "",
      userId: "",
      errors: [],
    };
  },
  methods: {
    movieNew: function () {
      var params = {
        title: this.title,
        plot: this.plot,
        year: this.year,
        // user_id: this.userId,
      };
      axios
        .post("/api/movies", params)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>