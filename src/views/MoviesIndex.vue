<template>
  <div class="movies-index">
    <div>
      <input
        type="text"
        v-model="search"
        list="titles"
        placeholder="Search..."
      />
      <datalist id="titles">
        <option v-for="movie in movies" v-bind:key="movie.title">{{
          movie.title
        }}</option>
      </datalist>
    </div>
    <div>
      <button v-on:click="sortattr = 'title'">Sort by Title</button>
    </div>
    <div
      v-for="movie in orderBy(filterBy(movies, search), sortattr, 'title')"
      v-bind:key="movie.id"
    >
      <h1>{{ movie.title }}</h1>
      <img src="movie.image" />
      <p>{{ movie.plot }}</p>
      <p>{{ movie.director }}</p>
      <p>{{ movie.year }}</p>
      <router-link :to="`/movies/${movie.id}`">More info</router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      movies: [],
      search: "",
      sortattr: ""
    };
  },
  created: function() {
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
  methods: {}
};
</script>
