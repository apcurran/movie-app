<template>
  <div class="movie-items">
    <article v-for="movie in movieResults" :key="movie.id" class="home-movie">
      <h2 class="home-movie-title">{{ movie.title }}</h2>
      <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" class="home-movie-img">
    </article>
  </div>
</template>

<script>
export default {
  name: 'MovieItem',
  props: ["movieResults"],
  data() {
    return {
      
    }
  }
}
</script>

<style>

.movie-items {
  margin: 0 auto;
  width: 70rem;
  max-width: 90%;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.home-movie {
  display: flex;
  flex-direction: column;
}

.home-movie-img {
  width: 100%;
}

</style>
