<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">
            <VideoDetail :video="selectedVideo"></VideoDetail>
            <VideoList :videos="videos" @videoSelect="onVideoSelect"></VideoList>
        </div>
        <!-- v-bind:videos can be changed to :input with same function -->
        <!-- {{ videos.length }} -->
    </div>    
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import VideoList from './components/VideoList.vue';
import VideoDetail from './components/VideoDetail.vue';
const API_KEY = 'AIzaSyAoWNUFzRglzqMUWA7navFcgFZ7DBRKGJM';

export default {
    name: 'App',
    // computed: {}, Only put if needed
    components: {
    SearchBar,
    VideoList,
    VideoDetail
},
    data() {
        return { videos: [], selectedVideo: null };
    },
    methods: {
        onVideoSelect(video){
            this.selectedVideo = video;
        },
        onTermChange(searchTerm) {
            axios
                .get('https://www.googleapis.com/youtube/v3/search', {
                    params: {
                        key: API_KEY,
                        type: 'video',
                        part: 'snippet',
                        q: searchTerm
                    }
                })
                .then(response => {
                    this.videos = response.data.items
                });
        }
    },
};
</script>