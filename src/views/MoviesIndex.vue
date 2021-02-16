<template>
  <div class="movies-index">
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h1>{{ movie.title }}</h1>
      <p>Year: {{ movie.year }} </p>
      <p>Plot: {{ movie.plot }} </p>
      <p>Director: {{ movie.director }} </p>
      <router-link to="/movies/show">More Info</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    axios
      .get("/api/movies")
      .then((response) => {
        console.log(response.data);
        this.movies = response.data;
      })
      .catch((error) => {
        console.log(error.response.data.errors);
      });
  },
  methods: {},
};
</script>