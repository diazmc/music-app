<template>
  <div id="app">
    <Navigation />
    <SongPlayer />
    <Playlist />
  </div>
</template>

<script>
import Navigation from './components/navigation/navigation'
import SongPlayer from './components/song-player/song-player'
import Playlist from './components/playlist/playlist'

export default {
  name: 'App',
  components: {
    Navigation,
    SongPlayer,
    Playlist
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

#app {
  height: 100vh;
  background-color: #0D0D15;
  color: #ffffff;
}
</style>
