<template>
    <div class="thumbnails">
        <div v-for="movie in movies" v-bind:key="movie" >
            <div class="poster" @click="changeCurrent(movie)">
            <img src="movie.poster" height="200" alt="">
            </div>
        </div>
  </div>
</template>



