<template>
  <div class="home">
    <Header/>
    <form @submit.prevent="getMovies" class="home-form">
      <input v-model="userSearch" type="text" class="home-form-search" placeholder="Search movie title">
      <input type="submit" value="Get Movies!" class="home-form-submit">
    </form>
    <section class="movie-items">
      <article @click="showMovieDetails(movie)" v-for="movie in movieResults" :key="movie.id" class="home-movie">
        <h2 class="home-movie-title">{{ movie.title }}</h2>
        <img v-if="movie.poster_path" :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" class="home-movie-img">
        <img v-else src="../assets/movie-poster-placeholder.jpg" alt="Movie reel placeholder" class="home-movie-img">
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

.home {
  min-height: 100vh;
  background-color: #fefefe;
}

.home-form {
  margin: 4rem auto 0 auto;
  width: 30rem;
  max-width: 90%;
  display: flex;
  justify-content: center;
}

.home-form-search {
  flex: 1 1;
  font-size: 1rem;
  padding: 0 .75rem;
  border: 1px solid #cbd5e0;
  border-right: none;
  border-radius: 500px 0 0 500px;
}

.home-form-search::placeholder {
  color: #ababab;
}

.home-form-submit {
  font-size: 1rem;
  font-weight: 500;
  padding: .75rem 1.75rem;
  text-transform: uppercase;
  letter-spacing: .04em;
  background-color: #9ae6b4;
  border: none;
  border-radius: 0 500px 500px 0;
  cursor: pointer;
}

.movie-items {
  margin: 4rem auto;
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
  padding: 1.5rem;
  border-radius: 4px;
  cursor: pointer;
  transition: box-shadow 120ms ease;
}

.home-movie:hover {
  box-shadow: 0 6px 18px rgba(0, 0, 0, .2);
}

.home-movie-title {
  font-size: 1.4rem;
  font-weight: 400;
  margin-bottom: 1.25rem;
}

.home-movie-img {
  width: 100%;
}

@media screen and (max-width: 28em) {
    .home-form { margin-top: 2.5rem; }

    .home-form-search {
      padding: .75rem 1rem;
      font-size: .9rem;
    }

    .home-form-submit {
      padding: .75rem 1rem;
      font-size: .925rem;
    }
}
</style>