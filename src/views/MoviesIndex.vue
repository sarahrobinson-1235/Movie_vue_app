<template>
  <div class="movies-index">
    <div class="jumbotron">
      <h1 class="display-4">Welcome to the Movie App!</h1>
      <p class="lead">
        Explore our selection of films..
      </p>
      <hr class="my-4" />
      <p>
        Add your favorite movie..
      </p>
      <router-link class="btn btn-success btn-block" :to="`/movies/new`"
        >Start here!</router-link
      >
    </div>

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
      <button class="btn btn-primary btn-sm" v-on:click="sortattr = 'title'">
        Sort by Title
      </button>
    </div>
    <div class="row">
      <div
        v-for="movie in orderBy(filterBy(movies, search), sortattr, 'title')"
        v-bind:key="movie.id"
        class="col-sm-6"
      >
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">
              {{ movie.plot }}
            </p>
            <router-link :to="`/movies/${movie.id}`">More info</router-link>
          </div>
        </div>
      </div>
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
      sortattr: "",
    };
  },
  created: function() {
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
