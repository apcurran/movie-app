<template>
  <div class="home">
    <header class="header">
      <h1 class="header-home-title">Video 2000</h1>
    </header>
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
    }
  }
}
</script>

<style>

.header-home-title {
  margin: 3rem 0;
  text-align: center;
}

.home-form {
  margin: 0 auto 4rem auto;
  width: 30rem;
  max-width: 90%;
  display: flex;
  justify-content: center;
}

.home-form-search {
  flex: 1 1;
  font-size: 1rem;
  padding: 0 .75rem;
}

.home-form-submit {
  font-size: 1rem;
  padding: .75rem 1.75rem;
}

</style>