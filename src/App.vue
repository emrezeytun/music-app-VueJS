<template>

<div>

  <div class="container">
<div class="row">
    <div class="col-md-6 left-area">

<p :class="{'active' : activeItem[song.id]} " class="list " @click="playMusic(index)" v-for="(song, index) in songs" :key="song.id"> {{ song.name }} - {{ song.artist }} </p>
</div>

<div class="col-md-6 right-area">

<img :src="songs[index].image" class="img-fluid" alt="">
<div>
<svg :class="{'no-allow' : isFirst}" @click="prevMusic" xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#fff" class="bi bi-arrow-left-circle-fill" viewBox="0 0 16 16">
  <path d="M8 0a8 8 0 1 0 0 16A8 8 0 0 0 8 0zm3.5 7.5a.5.5 0 0 1 0 1H5.707l2.147 2.146a.5.5 0 0 1-.708.708l-3-3a.5.5 0 0 1 0-.708l3-3a.5.5 0 1 1 .708.708L5.707 7.5H11.5z"/>
</svg>

<svg @click="continueMusic" v-show="!listening" xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#fff" class="bi bi-play-circle-fill" viewBox="0 0 16 16">
  <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM6.79 5.093A.5.5 0 0 0 6 5.5v5a.5.5 0 0 0 .79.407l3.5-2.5a.5.5 0 0 0 0-.814l-3.5-2.5z"/>
</svg>

<svg @click="pauseMusic" v-show="listening" xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#fff" class="bi bi-pause-circle-fill" viewBox="0 0 16 16">
  <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM6.25 5C5.56 5 5 5.56 5 6.25v3.5a1.25 1.25 0 1 0 2.5 0v-3.5C7.5 5.56 6.94 5 6.25 5zm3.5 0c-.69 0-1.25.56-1.25 1.25v3.5a1.25 1.25 0 1 0 2.5 0v-3.5C11 5.56 10.44 5 9.75 5z"/>
</svg>


<svg :class="{'no-allow' : isLast}" @click="nextMusic" xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#fff" class="bi bi-arrow-right-circle-fill" viewBox="0 0 16 16">
  <path d="M8 0a8 8 0 1 1 0 16A8 8 0 0 1 8 0zM4.5 7.5a.5.5 0 0 0 0 1h5.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3a.5.5 0 0 0 0-.708l-3-3a.5.5 0 1 0-.708.708L10.293 7.5H4.5z"/>
</svg>
</div>
<p  class="playingRight">  {{ songs[index].name }} - {{ songs[index].artist }} </p>

</div>
</div>
</div>
</div>

</template>

<script>

export default {
  name: 'App',

  data() {
    return {
     
      index: 0,
      audioElement : new Audio(),
      listening: false,
      activeItem: [],
      isLast: false,
      isFirst: false,
      songs: [
        { id:0 ,  name:  'We Are One', artist: 'Vexento', source: require ('./assets/we-are-one-vexento-no-copyright-music.mp3'), image: require ('./assets/vexento.jpg') },
        { id: 1, name:  'Echoes', artist: 'Atch', source: require ('./assets/echoes-atch-no-copyright-music.mp3'), image: require ('./assets/atch.jpg')},
        { id: 2, name:  'Buddha', artist: 'Kontekst', source: require ('./assets/buddha-kontekst-no-copyright-music.mp3'), image: require ('./assets/buddha.jpg')},
        { id: 3, name:  'Ancient', artist: 'Persian', source: require ('./assets/epic-arabian-music-ancient-persian-no-copyright.mp3'), image: require ('./assets/ancient.jpg')},
        { id: 4, name:  'Flying High', artist: 'Fredji', source: require ('./assets/flying-high-fredji-no-copyright-music.mp3'), image: require ('./assets/flying.jpg')},
        { id: 5, name:  'Summertime', artist: 'Erik Lund', source: require ('./assets/erik-lund-summertime-vlog-no-copyright-music.mp3'), image: require ('./assets/atch.jpg')},
        { id: 6, name:  'Cold Sun', artist: 'Del No', source: require ('./assets/cold-sun-del-no-copyright-music.mp3'), image: require ('./assets/cold_sun.jpg')},
        { id: 7, name:  'Jim Yosef', artist: 'Cant Wait', source: require ('./assets/Jim-Yosef-Cant-Wait.mp3'), image: require ('./assets/kim_josef.jpg')},
        { id:8 ,  name:  'We Are One', artist: 'Vexento', source: require ('./assets/we-are-one-vexento-no-copyright-music.mp3'), image: require ('./assets/vexento.jpg') },
        { id: 9, name:  'Echoes', artist: 'Atch', source: require ('./assets/echoes-atch-no-copyright-music.mp3'), image: require ('./assets/atch.jpg')},
        { id: 10, name:  'Buddha', artist: 'Kontekst', source: require ('./assets/buddha-kontekst-no-copyright-music.mp3'), image: require ('./assets/buddha.jpg')},
        { id: 11, name:  'Ancient', artist: 'Persian', source: require ('./assets/epic-arabian-music-ancient-persian-no-copyright.mp3'), image: require ('./assets/ancient.jpg')},
        { id: 12, name:  'Flying High', artist: 'Fredji', source: require ('./assets/flying-high-fredji-no-copyright-music.mp3'), image: require ('./assets/flying.jpg')},
        { id: 13, name:  'Summertime', artist: 'Erik Lund', source: require ('./assets/erik-lund-summertime-vlog-no-copyright-music.mp3'), image: require ('./assets/atch.jpg')},
        { id: 14, name:  'Cold Sun', artist: 'Del No', source: require ('./assets/cold-sun-del-no-copyright-music.mp3'), image: require ('./assets/cold_sun.jpg')},
        { id: 15, name:  'Jim Yosef', artist: 'Cant Wait', source: require ('./assets/Jim-Yosef-Cant-Wait.mp3'), image: require ('./assets/kim_josef.jpg')},
        { id:16 ,  name:  'We Are One', artist: 'Vexento', source: require ('./assets/we-are-one-vexento-no-copyright-music.mp3'), image: require ('./assets/vexento.jpg') },
        { id: 17, name:  'Echoes', artist: 'Atch', source: require ('./assets/echoes-atch-no-copyright-music.mp3'), image: require ('./assets/atch.jpg')},
        { id: 18, name:  'Buddha', artist: 'Kontekst', source: require ('./assets/buddha-kontekst-no-copyright-music.mp3'), image: require ('./assets/buddha.jpg')},
        { id: 19, name:  'Ancient', artist: 'Persian', source: require ('./assets/epic-arabian-music-ancient-persian-no-copyright.mp3'), image: require ('./assets/ancient.jpg')},
        { id: 20, name:  'Flying High', artist: 'Fredji', source: require ('./assets/flying-high-fredji-no-copyright-music.mp3'), image: require ('./assets/flying.jpg')},
        { id: 21, name:  'Summertime', artist: 'Erik Lund', source: require ('./assets/erik-lund-summertime-vlog-no-copyright-music.mp3'), image: require ('./assets/atch.jpg')},
        { id: 22, name:  'Cold Sun', artist: 'Del No', source: require ('./assets/cold-sun-del-no-copyright-music.mp3'), image: require ('./assets/cold_sun.jpg')},
        { id: 23, name:  'Jim Yosef', artist: 'Cant Wait', source: require ('./assets/Jim-Yosef-Cant-Wait.mp3'), image: require ('./assets/kim_josef.jpg')},
      ],
      viaJS : require('./assets/logo.png')
    }
  },
  methods: {
    
    pauseMusic() {
     this.listening = false;
     this.audioElement.pause();
    },
    continueMusic() {
     this.listening = true;
     this.audioElement.play();
    },
    playMusic(ind) {
      
      this.activeItem.splice(0, this.songs.length);
      this.activeItem[ind] = true;
      this.listening = true;
      this.index = ind;
      this.audioElement.src = this.songs[this.index].source;
      this.audioElement.pause();
      this.audioElement.play();
      this.index == this.songs.length-1 ? this.isLast = true : this.isLast = false;
      this.index == 0 ? this.isFirst = true : this.isFirst = false;
    },
    nextMusic() {
      this.index++;
      this.playMusic(this.index);
    },
    prevMusic() {
      this.index--;
      this.playMusic(this.index);
    }
  },
  created() {
    this.playMusic(this.index);
    this.listening=false;
    
  }
  
}


</script>

<style>
* {
  padding: 0;
  margin: 0;
}
body {
  background: #1e6f5c;
  font-family: 'Roboto', sans-serif;
  
}

svg {
  margin: 0px 7px;
  cursor: pointer;
  transition: .6s ease;
}

svg:hover {
  opacity: .8;
}

.left-area {
  margin-top: 2rem;
  height: 90vh !important;
  overflow: scroll;
  overflow-x: hidden;
}

.left-area::-webkit-scrollbar {
    width: 7px;
}

.left-area::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 5px rgba(0,0,0,0.3); 
    -webkit-border-radius: 10px;
    border-radius: 10px;
}

.left-area::-webkit-scrollbar-thumb {
    -webkit-border-radius: 10px;
    border-radius: 10px;
    background: rgba(0,0,0,0.4); 
    -webkit-box-shadow: inset 0 0 2px rgba(0,0,0,0.5); 
}



.list {
  background-color: rgba(0,0,0,0.3);
  padding: 0.4rem 1.2rem;
  border-radius: 1rem;
  margin: 0.4rem;
}

.active {
  background-color: rgba(0,0,0,0.6);
}

.right-area {
  display: flex;
  flex-direction: column;
  text-align: center;
  align-items: center;
  justify-content: center;
  
}
img {
 margin-bottom: 1rem;
  border-radius: 50%;
  border: 3px solid #fff;
  opacity: 0.8;

}

.playingRight {
  padding-top: 0.6rem;
  cursor:default;
  transition: .6s;
}

.no-allow {
  opacity: .3;
  cursor: not-allowed;
}

.no-allow:hover {
  opacity: .3;
}


p {
  color: #fff;
  font-size: 1rem;
  font-weight: 400;
  cursor: pointer;
}
</style>
