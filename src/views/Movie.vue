<template>
    <div class="movie">
        <Header/>
        <section class="movie-info">
            <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" :alt="movie.title" class="movie-info-img">
            <div class="movie-info-container">
                <h1 class="movie-info-title">{{ movie.title }}</h1>
                <h3 class="movie-info-release">Released: {{ movie.release_date }}</h3>
                <h3 class="movie-info-votes">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="30" height="30"><path class="star-icon" d="M6.1 21.98a1 1 0 0 1-1.45-1.06l1.03-6.03-4.38-4.26a1 1 0 0 1 .56-1.71l6.05-.88 2.7-5.48a1 1 0 0 1 1.8 0l2.7 5.48 6.06.88a1 1 0 0 1 .55 1.7l-4.38 4.27 1.04 6.03a1 1 0 0 1-1.46 1.06l-5.4-2.85-5.42 2.85zm4.95-4.87a1 1 0 0 1 .93 0l4.08 2.15-.78-4.55a1 1 0 0 1 .29-.88l3.3-3.22-4.56-.67a1 1 0 0 1-.76-.54l-2.04-4.14L9.47 9.4a1 1 0 0 1-.75.54l-4.57.67 3.3 3.22a1 1 0 0 1 .3.88l-.79 4.55 4.09-2.15z"/></svg>
                    <span class="movie-info-votes--big">{{ movie.vote_average }}</span>/10 based on {{ movie.vote_count }} votes
                </h3>
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
    background-color: #fefefe;
}

.movie-info-title {
    font-size: 2.1rem;
}

.movie-info {
    padding: 0 8rem;
    display: grid;
    grid-template-columns: 1fr 1.25fr;
    grid-template-rows: 1fr;
    justify-items: center;
    align-items: center;
    gap: 1.5rem 0;
}

.movie-info-img {
    width: 50%;
    border-radius: 4px;
    justify-self: end;
}

.movie-info-container {
    max-width: 40rem;
}

.movie-info-release {
    margin-top: .5rem;
    font-size: 1rem;
    color: hsl(210, 11%, 60%);
}

.movie-info-votes {
    margin-top: 1rem;
    margin-bottom: 2rem;
    font-weight: 400;
    color: hsl(210, 11%, 60%);
}

.movie-info-votes svg {
    margin-right: .4rem;
}

.star-icon {
    fill: hsl(47, 81%, 50%);
}

.movie-info-votes--big {
    font-size: 2.25rem;
    color: #000;
}

.movie-info-desc {
    line-height: 1.6;
}

@media screen and (max-width: 107em) {
    .movie-info {
        padding: 0 5rem;
    }

    .movie-info-img {
        width: 80%;
    }

    .movie-info-container {
        margin: 0 3rem;
    }
}

@media screen and (max-width: 62.5em) {
    .movie-info {
        padding: 0 3rem;
    }

    .movie-info-img {
        width: 100%;
    }
}

@media screen and (max-width: 44em) {
    .movie-info {
        padding: 4rem 1.75rem;
        grid-template-columns: 1fr;
    }

    .movie-info-container {
        margin: 0;
    }
}

</style>