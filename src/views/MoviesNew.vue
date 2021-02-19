<template>
  <div class="movies-new">
    <form v-on:submit.prevent="createMovie()">
      <h1>Add New Movie</h1>
      Title: <input type="text" v-model="title" />
      <br />
      Director: <input type="text" v-model="director" />
      <br />
      Plot: <input type="text" v-model="plot" />
      <br />
      <small>
        {{ 700-plot.length }} characters remaining
      </small> <br/>
      Year: <input type="text" v-model="year" />
      <input type="submit" class="btn btn-primary" value="Create" />
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
