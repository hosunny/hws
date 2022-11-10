<template>
  <div id="app">
    <h1>My First Youtube Project</h1>
    <TheSearchBar @search-video="createList" />
    <VideoDetail
    v-if="videoId"
    :videoId="videoId"
    />
    <VideoList 
    v-if="videos"
    :videos="videos.items"
    @videoGo="videoGo"
    />
  </div>
</template>

<script>
import TheSearchBar from './components/TheSearchBar.vue'
import VideoDetail from './components/VideoDetail.vue'
import VideoList from './components/VideoList.vue'
import axios from 'axios'
const angel = 'AIzaSyCQVwXRVJADLddvODbLZ0tCX6LiaB49MF0'

export default {
  name: 'App',
  components: {
    VideoList,
    VideoDetail,
    TheSearchBar,
  },
  data() {
    return {
      videos: null,
      videoId: null,
    }
  },
  
  methods: {
    createList(videoTitle) {
      const params= {
        part: 'snippet',
        key: angel,
        q: videoTitle,
        type: 'video'
      }
      console.log(angel)
      axios.get('https://www.googleapis.com/youtube/v3/search', { params })
      .then((response) => {
        this.videos = response.data
        
      })
      .catch()
    },
    videoGo(gogo) {
      this.videoId = gogo

    }
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
  margin-top: 60px;
}
</style>
