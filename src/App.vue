<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <router-link class="navbar-brand" to="/">Home</router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/movies">Movies</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" v-if="!loggedIn()" to="/signup"
              >Signup</router-link
            >
          </li>
          <li class="nav-item">
            <router-link class="nav-link" v-if="!loggedIn()" to="/login"
              >Login</router-link
            >
          </li>
          <li class="nav-item">
            <router-link class="nav-link" v-if="loggedIn()" to="/logout"
              >Logout</router-link
            >
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/movies/new"
              >New Movie</router-link
            >
          </li>
        </ul>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  methods: {
    loggedIn: function() {
      return localStorage.getItem("jwt");
    },
  },
};
</script>
