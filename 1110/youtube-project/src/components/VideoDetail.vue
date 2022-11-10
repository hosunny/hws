<template>
  <div>
    <iframe 
      id="ytplayer" 
      type="text/html" 
      width="640" 
      height="360"
      :src="videoUrl"
      frameborder="0"
      >
    </iframe>
  </div>
  
</template>

<script>
export default {
  name: 'VideoDetail',
  props: {
    videoId: String
  },
  computed: {
    videoUrl() {
      return "https://www.youtube.com/embed/" + this.videoId
    }
  }
}
</script>

<style>

</style>