<template>
  <div class="movies-edit">
    <form v-on:submit.prevent="updateMovie()">
      <label for="movie">Title</label>
      <input id="movie" type="text" v-model="movie.title" /> <br />
      <label for="movie">Director</label>
      <input id="movie" type="text" v-model="movie.director" /> <br />
      <label for="movie">Plot</label>
      <input id="movie" type="text" v-model="movie.plot" /> <br />
      <label for="movie">Year</label>
      <input id="movie" type="text" v-model="movie.year" /> <br />
      <input v-on:click="updateMovie(movie)" type="submit" value="Update" />
      <input v-on:click="destroyMovie(movie)" type="button" value="Delete" />
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function() {
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
  methods: {
    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.plot,
        director: movie.director,
      };
      axios
        .patch(`/api/movies/${this.movie.id}`, params)
        .then((response) => {
          console.log(response.data);
          this.$router.push(`/movies/${this.movie.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
    destroyMovie: function() {
      if (confirm("Are you sure you want to delete this movie?")) {
        axios.delete(`/api/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
      }
    },
  },
};
</script>
