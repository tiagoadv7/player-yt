<template>
  <div id="app">
    <div v-if="!fullscreen" class="container">
      <input v-model="videoUrl" placeholder="Insira URL do YouTube" />
      <button @click="playVideo">Iniciar Video</button>
    </div>
    <div v-if="fullscreen" class="fullscreen-container" >
      <youtube :video-id="videoId" :player-vars="playerVars"></youtube>
    </div>
  </div>
</template>

<script>
import YouTube from 'vue-youtube';
//import Youtube from 'path-to-youtube-component';
export default {
  components: {
    YouTube
  },
  data() {
    return {
      videoUrl: '',
      videoId: '',
      fullscreen: false,
      
      playerVars: {
        //fullscreen: true,
        autoplay: 1
      }
    };
  },
  methods: {
    getYouTubeVideoId(url) {
      const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=)([^#\&\?]*).*/;
      const match = url.match(regExp);
      return (match && match[2].length === 11) ? match[2] : null;
      
    },
    playVideo() {
      this.videoId = this.getYouTubeVideoId(this.videoUrl);
      if (this.videoId) {
        this.fullscreen = true;
        this.$nextTick(() => {
          const iframe = this.$el.querySelector('iframe');
          if (iframe) {
            iframe.fullscreenContent('.iframe-container',);
            frameborder="0"
            allowfullscreen
          }
        });
      } else {
        alert('Insira uma URL válida!');
        this.$fullscreen.toggle(allowfullscreen)
      }
    }
  },
};

</script>
<!--script>
export default {
  name: 'Tutorial',
  methods: {
    openFullScreen() {
      const youtubePlayer = this.$refs.youtubePlayer.$el;
      if (youtubePlayer.requestFullscreen) {
        youtubePlayer.requestFullscreen();
      } else if (youtubePlayer.mozRequestFullScreen) { // Firefox
        youtubePlayer.mozRequestFullScreen();
      } else if (youtubePlayer.webkitRequestFullscreen) { // Chrome, Safari and Opera
        youtubePlayer.webkitRequestFullscreen();
      } else if (youtubePlayer.msRequestFullscreen) { // IE/Edge
        youtubePlayer.msRequestFullscreen();
      }
    }
  }
}
</script-->
<style>
.container {
  text-align: center;
  margin-top: 20px;
}
.fullscreen-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: black;
  display: flex;
  justify-content: center;
  align-items: center;
  object-fit: cover;
}
</style>
