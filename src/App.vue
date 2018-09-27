<style lang="css" scoped>



</style>

<template lang="html">

<div class="container">
    <SearchBar @termChange="onTermChange"></SearchBar>
    <div class="row">
        <VideoDetail :video="selectedVideo" />
        <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
    </div>
</div>

</template>

<script>

const API_KEY = "AIzaSyCY0VovjZkEjpCAl1nZYIb56Fh-dxz9ry8";
import SearchBar from "./components/SearchBar";
import VideoDetail from "./components/videoDetail";
import VideoList from "./components/videoList.vue";
import axios from "axios";

export default {
    name: "App",
    data() {
        return {
            videos: [],
            selectedVideo: null
        };
    },
    methods: {
        onVideoSelect(video) {
                this.selectedVideo = video;
            },
            onTermChange(searchTerm) {
                axios
                    .get("https://www.googleapis.com/youtube/v3/search", {
                        params: {
                            key: API_KEY,
                            type: "video",
                            part: "snippet",
                            q: searchTerm
                        }
                    })
                    .then(response => (this.videos = response.data.items));
            }
    },
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    }
};

</script>
