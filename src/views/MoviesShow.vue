<template>
  <div class="movies-show">
    <div>
      {{ movie }}
      <h1>title: {{ movie.title }}</h1>
      <p>movie id: {{ movie.id }}</p>
      <p>year: {{ movie.year }}</p>
      <p>description: {{ movie.description }}</p>
    </div>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
    <button type="button" class="btn btn-danger" v-on:click="movieDestroy()">
      Delete movie
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
    };
  },
  created: function() {
    axios.get(`/api/movies/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    movieDestroy: function() {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios
          .delete(`/api/movies/${this.$route.params.id}`)
          .then((response) => {
            console.log(response.data);
            this.$router.push("/movies");
          });
      }
    },
  },
};
</script>
