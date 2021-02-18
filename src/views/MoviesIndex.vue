<template>
  <div class="movies-index">
    <div>Search:<input type="text" v-model="titleFilter" list="titles" /></div>
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">
        {{ movie.title }}
      </option>
    </datalist>
    <button v-on:click="setAttribute = 'title'">Sort by Title</button>
    <div
      v-for="movie in orderBy(
        filterBy(movies, titleFilter, 'title'),
        setAttribute
      )"
      v-bind:key="movie.id"
    >
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
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
      setAttribute: "",
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