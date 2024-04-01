<script lang="js" setup>
    const query = ref("batman");
    const movies = ref([]);
    async function search() {
        const { Search } = await $fetch(`https://www.omdbapi.com/?apikey=5ac57fc0&s=${query.value}`);
        movies.value = Search;
    }
    search()
</script>
<template>
    <div>
        <form @submit.prevent="search">
            <input type="text" v-model="query" />
            <button>Search</button>
        </form>
        <ul class="flex flex-row flex-wrap gap-6">
            <li 
                v-for="movie in movies" :key="movie.imdbID"
            >
                <NuxtLink :to="{ name: 'movies-id', params: { id: movie.imdbID } }">
                    <img :src="movie.Poster" :alt="movie.title">
                </NuxtLink>
            </li>
        </ul>
    </div>
</template>
