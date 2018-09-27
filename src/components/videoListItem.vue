<style lang="css" scoped>

li {
    display: flex;
    cursor: pointer;
    border: 1px solid gray;
}

li:hover {
    background-color: #eee;
}

</style>

<template lang="html">

<li @click="onVideoSelect" class="list-group-item media">

    <img :src="video.snippet.thumbnails.default.url" class="mr-3" />
    <div class="media-body">
        {{video.snippet.title}}
    </div>
</li>

</template>

<script>

export default {
    name: "VideoListItem",
    props: ["video"],
    computed: {
        thumbnailUrl() {
            return this.video.snippet.thumbnails.default.url;
        }
    },
    methods: {
        onVideoSelect() {
            this.$emit("videoSelect", this.video);
        }
    }
};

</script>
