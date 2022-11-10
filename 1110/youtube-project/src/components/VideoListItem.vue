<template>
    <li>
        <img :src="thumbUrl" alt="" @click="videoGo">
        <p @click="videoGo">{{ video.snippet.title }}</p>
    </li>
</template>

<script>
export default {
    name: 'VideoListItem',
    props: {
        video: Object,
    },
    methods: {
        videoGo() {
            this.$emit('videoGo', this.video.id.videoId)
        }
    },
    computed: {
        thumbUrl() {
            return this.video.snippet.thumbnails.default.url
        }
    }
}
</script>

<style>

</style>