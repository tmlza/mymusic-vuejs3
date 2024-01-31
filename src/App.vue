<template>
  <div id="App">
    <div class="body">
      <header>
        <h1>My Music App</h1>
      </header>
      <main>
        <section class="player">
          <h2 class="song-title">{{current.title}} - {{current.artist}}</h2>
          <!-- <h3>{{songs[1].src}}</h3> -->
        </section>
        <div class="controls">
          <button @click="prev" class="Prev">Prev</button>
          <button @click="play" class="Pre" v-if="!isplaying">Play</button>
          <button @click="pause" class="Pre" v-else>Pause</button>
          <button @click="next" class="Pre">Next</button>
        </div>
        <section class="playlist">
          <h3>Playlist</h3>
          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src? 'playing':'song')">{{song.title}} - {{song.artist}}</button>
        </section>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      current:{},
      index:0,
      isplaying:false,
      songs:[
        {title:'first song',artist:'Paulinho',src: require('./assets/better-day.mp3')},
        {title:'second song',artist:'Jesus',src: require('./assets/drive-breakbeat.mp3')},
        {title:'third song',artist:'Richarlison',src: require('./assets/realize-your-dreams.mp3')},
      ],
      player: new Audio('this.current')
    }
  },
  methods: {
    play(song) {
      // var audio = new Audio(require('./assets/realize-your-dreams.mp3'));
      // audio.play();
      if(typeof song.src != undefined) {
        this.current = song;
        this.player.src = this.current.src;
        this.player.play();
      }
      this.player.play();
      this.isplaying = true;
    },
    pause() {
      this.player.pause();
      // this.current = this.songs[this.index];
      this.isplaying = false;
    },
    next() {
      this.index++;
      if(this.index>this.songs.length-1) {
        this.index=0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
      this.isplaying = true;
    },
    prev() {
      this.index--;
      if(this.index<0) {
        this.index=this.songs.length-1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
      this.isplaying = true;
    },
    // changebtn(){
    //   this.isplaying = !this.isplaying;
    // }
  },
  created(){
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    // console.log(this.player.src);
    // this.player.src.play();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  
}

*{
  box-sizing: 0;
}

body {
  margin-top: 60px;
  margin: auto;
  width: 500px;
  height: 700px;
  background: #cbebf2;
}

header h1 {
  padding: 25px;
  background: #039fbe;
  color: white;
  font-size: large;
  display: flex;
  justify-content: center;
  align-items: center;
}

.controls button {
  cursor: pointer;
  margin-right: 7px;
}

.playlist {
  display: flex;
  flex-direction: column;
  justify-self: center;
  align-items: center;
}

.playlist button {
  padding: 17px;
  cursor: pointer;
  border-radius: 5px;
  margin-top: 5px;
  display: block;
}

.playlist .playing {
  background: #da8585;
}
</style>
