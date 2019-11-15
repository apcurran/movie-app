<template>
    <div class="movie">
        <Header/>
        <section class="movie-info">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" class="movie-info-img">
            <div class="movie-info-container">
                <h1 class="movie-info-title">{{ movie.title }}</h1>
                <h3 class="movie-info-release">{{ movie.release_date }}</h3>
                <h3 class="movie-info-votes">{{ movie.vote_average }}/10 based on {{ movie.vote_count }} votes</h3>
                <p class="movie-info-desc">{{ movie.overview }}</p>
            </div>
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

.movie {
    display: grid;
    grid-template-rows: auto 1fr;
    min-height: 100vh;
}

.movie-title {
    text-align: center;
}

.movie-info {
    padding: 0 8rem;
    display: grid;
    grid-template-columns: 1fr 1.25fr;
    grid-template-rows: 1fr;
    justify-items: center;
    align-items: center;
    gap: 1.5rem;
}

.movie-info-img {
    width: 50%;
    border-radius: 4px;
}

.movie-info-container {
    margin: 3rem;
}

</style>