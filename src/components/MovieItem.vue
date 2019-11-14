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
  cursor: pointer;
}

.home-movie-title {
  font-size: 1rem;
  margin-bottom: 1.25rem;
}

.home-movie-img {
  width: 100%;
}

</style>
