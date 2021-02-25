<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <label for="movie">Title</label>
      <input id="movie" type="text" v-model="title" /> <br>
      <label for="movie">Director</label>
      <input id="movie" type="text" v-model="director" /> <br>
      <label for="movie">Plot</label>
      <input id="movie" type="text" v-model="plot" /> <br>
      <label for="movie">Year</label>
      <input id="movie" type="text" v-model="year" /> <br>
      <label for="movie">Image</label>
      <input id="movie" type="text" v-model="image" /> <br>
      <input type="submit" value="Create" /> 
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      title: "",
      director: "",
      year: "",
      plot: "",
      image: "",
      errors: []
    };
  },
  methods: {
    createMovie: function() {
      var params = {
        title: this.title,
        director: this.director,
        year: this.year,
        plot: this.plot
      };
      axios
        .post("api/movies", params)
        .then(response => {
          console.log(response.data);
          this.$router.push("/movies");
        })
        .catch(error => {
          console.log(error.response.data.errors);
        });
    }
  }
};
</script>
