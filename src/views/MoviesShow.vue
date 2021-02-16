<template>
  <div class="movies-show">
    
      <h1>{{ movie.title }}</h1>
      <p>Year: {{ movie.year }} </p>
      <p>Plot: {{ movie.plot }} </p>
      <p>Director: {{ movie.director }} </p>
    
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios
      .get(`/api/movies/${this.$route.params.id}`)
      .then((response) => {
        this.movie = response.data;
        console.log(this.movie);
      })
      .catch((error) => {
        console.log(error.response.data.errors);
      });
  },
  methods: {},
};
</script>