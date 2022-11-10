<template>
  <div>
    <input 
        type="text"
        v-model="videoTitle"
        @keyup.enter="searchvideo"
    >
  </div>
</template>

<script>
export default {
    name: 'TheSearchBar',
    data() {
        return {
            videoTitle: null,
        }
    },
    methods: {
        searchvideo() {
            this.$emit('search-video', this.videoTitle)
            this.videoTitle = null
        }
    }
}
</script>

<style>

</style>