<template>
<div class="movies-index">
    <div v-for="movie in movies" :key="movie.id">
    <div class="row" v-for="movie in movies" :key="movie.id">
      <div class="col-sm-6">
        <div class="card">
          <div class="card-body">
            <router-link v-bind:to="`/movies/${movie.id}`">
              <h5 class="card-title">{{ movie.title }}</h5>
            </router-link>
            <p class="card-text">{{ movie.year }}</p>
            <p class="card-text">{{ movie.plot }}</p>
            <a href="/movies/${movie.id}" class="btn btn-primary">More info</a>
          </div>
        </div>
      </div>
    </div>
  <!-- <div class="movies-index">
    <div v-for="movie in movies" :key="movie.id">
      <router-link v-bind:to="`/movies/#{movie.id}`">
        <h2>Title: {{ movie.title }}</h2>
        <p>Plot: {{ movie.plot }}</p>
      </router-link>
    </div>
  </div> -->
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
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        this.movies = response.data;
        console.log("All movies:", this.movies);
      });
    },
  },
};
</script>