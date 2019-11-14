<template>
  <div class="home">
    <Header/>
    <form @submit.prevent="getMovies" class="home-form">
      <input v-model="userSearch" type="text" class="home-form-search" placeholder="Search movie title">
      <input type="submit" value="Get Movies!" class="home-form-submit">
    </form>
    <section class="movie-items">
      <article v-for="movie in movieResults" :key="movie.id" class="home-movie">
        <h2 class="home-movie-title">{{ movie.title }}</h2>
        <img v-if="movie.poster_path" :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" class="home-movie-img">
        <img v-else src="../assets/movie-poster-placeholder.jpg" alt="Movie reel placeholder" class="home-movie-img">
        <button @click="showMovieDetails(movie)" class="home-movie-info">More Info</button>
      </article>
    </section>
  </div>
</template>

<script>

import Header from "@/components/Header";

export default {
  name: 'Home',
  components: {
    Header
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
    },
    showMovieDetails(movie) {
      this.$router.push({ name: "Movie", params: { movie: movie } });
    }
  }
}
</script>

<style>

.home-form {
  margin: 3rem auto 0 auto;
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
  text-transform: uppercase;
  letter-spacing: .04em;
  cursor: pointer;
}

.movie-items {
  margin: 3rem auto;
  width: 70rem;
  max-width: 90%;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}

.home-movie {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: transparent;
  padding: 1.5rem;
  border-radius: 4px;
}

.home-movie:hover {
  background-color: #999;
}

.home-movie-title {
  font-size: 1rem;
  margin-bottom: 1.25rem;
}

.home-movie-img {
  width: 100%;
}

.home-movie-info {
  margin-top: 1.5rem;
  padding: .8rem 1.75rem;
  text-transform: uppercase;
  letter-spacing: .04em;
  cursor: pointer;
}

</style>