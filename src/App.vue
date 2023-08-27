<template>
  <v-app>
    <v-container>
      <h1 class="title text-center mb-4">Movies</h1>
      
      <v-text-field
        class="input-field"
        v-model="search"
        label="Search Movies"
        outlined
        dense
        color="primary"
        @input="fetchMovies"
      />

      <v-row class="card-movies" justify="center">
        <v-col cols="12" sm="6" md="4" lg="3" v-for="movie in movies" :key="movie.imdbID">
          <v-card class="movie-card">
            <v-img :src="movie.Poster" class="movie-poster"></v-img>
            <div class="movie-info">
              <h2 class="movie-title">{{ movie.Title }}</h2>
              <p class="movie-year">{{ movie.Year }}</p>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  name: 'App',
  components: {},
  data: () => ({
    search: 'fast',
    movies: []
  }),
  mounted() {
    this.fetchMovies();
  },
  methods: {
    fetchMovies() {
      axios.get(`https://www.omdbapi.com/?s=${this.search}&apikey=581359b4`)
        .then((response) => {
          this.movies = response.data.Search;
        });
    }
  }
};
</script>

<style scoped>
.title {
  color: #333;
  font-size: 24px;
  margin-bottom: 20px;
}

.input-field {
  margin-bottom: 20px;
}

.v-text-field--outlined {
  border-radius: 20px;
}

.v-label {
  color: #1976D2;
}

.v-icon {
  color: #1976D2;
}

.movie-card {
  background-color: #fff;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s, box-shadow 0.2s;
  margin: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  box-sizing: border-box;
}

.movie-poster {
  max-height: 300px;
}

.movie-info {
  text-align: center;
  margin-top: 15px;
}

.movie-title {
  font-size: 18px;
  margin: 0;
}

.movie-year {
  font-size: 14px;
  color: #888;
  margin: 0;
}
</style>