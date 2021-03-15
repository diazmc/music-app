<template>
  <div class="song-player">
    <h2 class="song-title">
      <span>{{currentSong.artist}} - </span>
      <span>{{currentSong.title}}</span>
    </h2>
    <div class="controls">
      <button class="prev" @click="prev">Prev</button>
      <button class="play" v-if="!isPlaying" @click="play">Play</button>
      <button class="pause" v-else @click="pause()">Pause</button>
      <button class="next" @click="next">Next</button>
    </div>
    <div class="playlist">
      <h3>The Playlist</h3>
      <button 
      v-for="song in songs" 
      :key='song.src' 
      @click='play(song)' 
      :class="(song.src === currentSong.src) ? 'song playing' : 'song'">
        {{song.title}} - {{song.artist}}
      </button>
    </div>
  </div>  
</template>

<script>
export default {
  props: {
  },
  data: () => ({
    currentSong: {},
    isPlaying : false,
    index: 0,
    songs: [
      {
        title: 'Juicy',
        artist: 'The Notorious B.I.G.',
        src: require('../../assets/notorious-big-juicy.mp3')
      },
      {
        title: 'Myself',
        artist: 'NAV',
        src: require('../../assets/nav-myself.mp3')
      }
    ],
    player: new Audio()
  }),
  methods: {
    play (song) {
      if (song.src != undefined) {
        this.currentSong = song;
        this.player.src = this.currentSong.src
      }
      this.player.volume = 0.1
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }

      this.currentSong = this.songs[this.index];
      this.play(this.currentSong);
    },
    prev () {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }

      this.currentSong = this.songs[this.index];
      this.play(this.currentSong);
    }
  },
  created () {
    this.currentSong = this.songs[this.index];
    this.player.src = this.currentSong.src;
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
