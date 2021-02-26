<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">Movie App</a>
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
            <router-link to="/movies">Movies | </router-link>
          </li>
          <li class="nav-item">
            <router-link to="/movies/new">Add Movie |</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!loggedIn()" to="/signup">Signup |</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="!loggedIn()" to="/login">Login |</router-link>
          </li>
          <li class="nav-item">
            <router-link v-if="loggedIn()" to="/logout">Logout</router-link>
          </li>
        </ul>
      </div>
    </nav>

    <div class="container">
      <!-- Content here -->
      <router-view />
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {};
  },
  methods: {
    loggedIn: function() {
      return localStorage.jwt;
    },
    getUserId: function() {
      return localStorage.user_id;
    },
  },
};
</script>
