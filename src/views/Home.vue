<template>
  <div class="home">
    <h1>Add New Movie</h1>
    Title: <input type="text" v-model="newTitle" />
    <br />
    Director: <input type="text" v-model="newDirector" />
    <br />
    Plot: <input type="text" v-model="newPlot" />
    <br />
    Year: <input type="text" v-model="newYear" /> <br />
    Image: <input type="text" v-model="newImage" />
    <button v-on:click="createMovie()">Create</button>
    <h1 title="Check out the Movies tab for more info">All Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h3 title="Check out the Movies tab for more info">{{ movie.title }}</h3>
      <p>Director: {{ movie.director }}</p>
      <p>Year: {{ movie.year }}</p>
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
      newTitle: "",
      newDirector: "",
      newYear: "",
      newPlot: "",
      newImage: ""
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios
        .get("/api/movies")
        .then(response => {
          console.log(response.data);
          this.movies = response.data;
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    },
    createMovie: function() {
      var params = {
        title: this.newTitle,
        director: this.newDirector,
        plot: this.newPlot,
        year: this.newYear
      };
      axios
        .post("http://localhost:3000/api/movies", params)
        .then(response => {
          console.log(response.data);
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    }
  }
};
</script>
