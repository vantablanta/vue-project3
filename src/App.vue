<template>
<div class="videos-container" id="app">
  <div class="video-player">
      <Frame 
      :source="current"
      />
  </div>

  <div class="video-choices">
    <Thumbnail 
    :movies="movies" v-on:choose-movie="handleChangeCurrent"
    />
  </div>
</div>

</template>

<script>

import Frame from './components/Frame.vue'
import Thumbnail from './components/Thumbnail.vue'
export default {
name: 'App',

components: {
   Frame,
   Thumbnail
  },

data() {
  return {
    api: "https://scotch-mvplayer-api.herokuapp.com/api/v1",
    movies: [],
    current: null
  }
  },
  props: ["source"],

created() {
    axios.get(this.api).then(res => {
      this.movies = res.data;
      this.current = this.movies[0]
    })
  },

methods: {
    handleChangeCurrent(movie) {
      this.current = movie
    },
    changeCurrent(movie) {
      this.$emit('choose-movie', movie)
  }
},

};

</script>

<style>
body {
  background: #1e3c72;
  background: linear-gradient(to right, #1e3c72, #2a5298);
  padding: 30px;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.videos-container {
  background: #333;
  padding: 10px;
  box-shadow: 0 0 50px 5px rgba(0, 0, 0, 0.25);
  color: #FFF;
}

.video-player   {
  min-height: 300px;
  width: 100%;
  background: #000;
  margin-bottom: 10px;
}

.video-choices  {
  display: flex;
}
  :not(:last-child) {
    margin-right: 5px;
  }

img {
    height: 100px;
   
}

.poster{
    float: left;
 }

.thumbnails{
  display: flex;
  justify-content: left;
}
</style>
