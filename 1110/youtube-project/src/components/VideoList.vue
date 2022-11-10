<template>
  <div>
    <ul>
      <VideoListItem 
        v-for="(video, index) in videos" 
        :key="index" 
        :video="video"
        @videoGo='videoGo'
        />
    </ul>
  </div>
</template>

<script>
import VideoListItem from '@/components/VideoListItem'

export default {
    name: 'VideoList',
    components: {
      VideoListItem
    },
    props: {
      videos: Array,
    },
    methods: {
      videoGo(gogo) {
            this.$emit('videoGo', gogo)
        }
    }
}
</script>

<style>

</style>