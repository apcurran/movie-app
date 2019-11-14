<template>
    <div class="movie">
        <Header/>
        <h1 class="title">Movie Page</h1>
        <section class="movie-info">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" class="movie-info-img">
            <h2 class="movie-info-title">{{ movie.title }}</h2>
            <h3 class="movie-info-release">{{ movie.release_date }}</h3>
            <h3 class="movie-info-votes">{{ movie.vote_average }}/10 based on {{ movie.vote_count }} votes</h3>
            <p class="movie-info-desc">{{ movie.overview }}</p>
        </section>
    </div>
</template>

<script>
import Header from "@/components/Header";

export default {
    name: "Movie",
    components: {
        Header
    },
    props: [
        "movie"
    ]
}
</script>

<style>



</style>