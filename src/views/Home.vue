<template>
  <div class="home">
    <h1 class="home-title">Hello World!</h1>
    <form @submit.prevent="getMovies" class="home-form">
      <input v-model="userSearch" type="text" class="home-form-search" placeholder="Search movie title">
      <input type="submit" value="Get Movies!" class="home-form-submit">
    </form>
    <MovieItem :movieResults="movieResults"/>
  </div>
</template>

<script>
import MovieItem from '@/components/MovieItem.vue'

export default {
  name: 'Home',
  components: {
    MovieItem
  },
  data() {
    return {
      userSearch: "",
      movieResults: []
    }
  },
  methods: {
    async getMovies() {
      const API_KEY = "c1bc2d59ec311674f1c2db8953212349";
      const userMovie = this.userSearch;
      const URL = `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&language=en-US&query=${userMovie}&page=1&include_adult=false`;

      try {
        const response = await fetch(URL, { mode: "cors" });
        const data = await response.json();
        this.displayMovies(data);
      }
      catch(err) {
        console.error(err);
      }
    },
    displayMovies(data) {
      this.movieResults = data.results;
      console.log(this.movieResults);
    }
  }
}
</script>
