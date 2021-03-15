<template>
  <div class="song-player">
    <h2 class="song-title">
      <span>{{currentSong.title}} - </span>
      <span>{{currentSong.artist}}</span>
    </h2>
    <div class="controls">
      <button class="prev">Prev</button>
      <button class="play" v-if="!isPlaying" @click="play(currentSong)">Play</button>
      <button class="pause" v-else @click="pause()">Pause</button>
      <button class="next">Next</button>
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
        src: '~/assets/notorious-big-juicy.mp3'
      },
      {
        title: 'Myself',
        artist: 'NAV',
        src: '~/assets/nav-myself.mp3'
      }
    ],
    player: new Audio()
  }),
  methods: {
    play (song) {
      if (typeof song.src !== "undefined") {
        this.currentSong = song;
        this.player.src = this.currentSong.src
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    }
  },
  created () {
    this.currentSong = this.songs[this.index];
    this.player.src = this.currentSong.src;
    // this.player.play()
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
