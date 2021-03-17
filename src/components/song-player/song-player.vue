<template>
  <div class="song-player">
    <h1>Playing Now</h1>

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
        title: 'Myself',
        artist: 'NAV',
        src: require('../../assets/nav-myself.mp3')
      },
      {
        title: 'Juicy',
        artist: 'The Notorious B.I.G.',
        src: require('../../assets/notorious-big-juicy.mp3')
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
      this.player.addEventListener('ended', () => {
        this.index++;
        if (this.index > this.songs.length - 1) {
          this.index = 0;
        }

        this.currentSong = this.songs[this.index];
        this.play(this.currentSong);
      })
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
.song-player {
  margin: 0 auto;
  text-align: center;
  width: 50%;
}

.song-player h1 {
  margin: 2rem 0;
}

button {
	background:linear-gradient(to bottom, #44c767 5%, #5cbf2a 100%);
	background-color:#44c767;
	border-radius:28px;
	border:1px solid #18ab29;
	display:inline-block;
	cursor:pointer;
	color:#ffffff;
  transition: background .35s ease;
	font-family:Arial;
	font-size:16px;
	padding:16px 31px;
	text-decoration:none;
	text-shadow:0px 1px 0px #2f6627;
}
button:hover {
	background:linear-gradient(to bottom, #5cbf2a 5%, #44c767 100%);
	background-color:#5cbf2a;
  cursor: pointer;
}
button:active {
	position:relative;
	top:1px;
}

button:focus{
  outline: 0;
}

.play, .pause {
  font-size: 2rem;
}


.controls button:not(:last-of-type) {
  margin-right: 2rem;
}

.playlist {
  display: flex;
  flex-direction: column;
}

.playlist > * {
  margin-bottom: 2rem;
}

.song-title,
.controls,
.playlist {
  margin-bottom: 2rem;
}
</style>
