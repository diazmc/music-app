<template>
  <div id="app">
    <Navigation />
    <SongPlayer />
  </div>
</template>

<script>
import Navigation from './components/navigation/navigation'
import SongPlayer from './components/song-player/song-player'

export default {
  name: 'App',
  components: {
    Navigation,
    SongPlayer
  },
  data () {
    return {
      
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: 'montserrat', sans-serif;
}

/* #app {
  background-image: url('./assets/')
} */
</style>
