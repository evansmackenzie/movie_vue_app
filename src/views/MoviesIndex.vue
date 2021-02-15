<template>
  <div class="movies-index">
    <div v-for="movie in movies"  v-bind:key="movie.id">
      <h1>Title: {{ movie.title }}</h1>
      <p>plot: {{ movie.plot }}</p>
      <p>year: {{ movie.year }}</p>
      <p>director: {{ movie.director }}</p>
      <p>english? {{ movie.english }}</p>
      <p>genres: {{ movie.genres }}</p>
      <router-link :to="`movies/${movie.id}`">More Info</router-link>
    </div>

    <!-- <div>
      <button v-on:click="createMovie">Add Movie</button>

    </div> -->
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/api/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    // createMovie: function () {
    //   var params = {
    //     title: "Seven Samurai",
    //     year: 1957,
    //     plot: "Seven samurai protect a village.",
    //     director: "Akira Kurosawa",
    //     english: false,
    //   };
    //   axios
    //     .post("http://localhost:3000/api/movies", params)
    //     .then((response) => {
    //       this.movies.push(response.data);
    //     });
    // },
  },
};
</script>