<template>
  <div class="home">
    <div class="jumbotron">
      <h1 class="display-4">Marvelous Movies Website!</h1>
      <p class="lead">
        This website gives you a list of movies and summarizes them! You can
        also create and destroy movies!
      </p>
      <hr class="my-4" />
    </div>
    <div>
      <button
        type="button"
        class="btn btn-outline-primary"
        v-on:click="createMovie"
      >
        Add Movie
      </button>
    </div>

    <div v-for="movie in movies" v-bind:key="movie.id">
      <h1>Title: {{ movie.title }}</h1>
      <p>plot: {{ movie.plot }}</p>
      <p>year: {{ movie.year }}</p>
      <p>director: {{ movie.director }}</p>
      <p>english? {{ movie.english }}</p>
      <p>genres: {{ movie.genres }}</p>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movies: [],
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("http://localhost:3000/api/movies").then((response) => {
        this.movies = response.data;
      });
    },
    createMovie: function() {
      var params = {
        title: "Seven Samurai",
        year: 1957,
        plot: "Seven samurai protect a village.",
        director: "Akira Kurosawa",
        english: false,
      };
      axios
        .post("http://localhost:3000/api/movies", params)
        .then((response) => {
          this.movies.push(response.data);
        });
    },
  },
};
</script>
