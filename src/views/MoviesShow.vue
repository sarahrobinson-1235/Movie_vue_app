<template>
  <div class="movies-show">
    <h1>{{ movie.title }}</h1>
    <h2>{{ movie.plot }}</h2>
    <p>Director: {{ movie.director }}</p>
    <p>Year: {{ movie.year }}</p>
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
      errors: []
    };
  },
  created: function() {
    axios
      .get(`/api/movies/${this.$route.params.id}`)
      .then(response => {
        this.movie = response.data;
        console.log(this.movie);
      })
      .catch(error => {
        console.log(error.response.data.errors);
      });
  },
  methods: {}
};
</script>
