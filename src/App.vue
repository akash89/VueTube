<template>
    <div class="wrapper">
        <div class="title-wrapper">
            <h1 class="title">Vue<span>Tube</span></h1>
        </div>
        <div class="app-container">
            <SearchBar @termChange="onTermChange"></SearchBar>
            <div class="row">
                <VideoDetail :video="selectedVideo"/>
                <VideoList 
                    @videoSelect="onVideoSelect"
                    :videos="videos">
                </VideoList>
            </div>
        </div>
    </div>
</template>

<script>

// Vue Component (Not a Vue Instance)
// @ means v-on:
// : means v-bind: 

import axios from 'axios';
import SearchBar from './components/SearchBar';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

const API_KEY = process.env.VUE_APP_API_KEY;

export default {
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail
    },
    data() {
        return {
            videos: [],
            selectedVideo: null
        };
    },
    methods: {
        onTermChange(searchTerm) {
            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key: API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm
                }
            }).then(response => {
                this.videos = response.data.items;
            });
        },
        onVideoSelect(video) {
            this.selectedVideo = video;
        }
    }
};
</script>

<style scoped>
.wrapper {
    min-height: 100vh;
    /* background: radial-gradient(ellipse at center, #fff 0%,#D9F7DA 100%); */
    /* background: radial-gradient(ellipse at center, #1b2735 0%,#090a0f 100%); */
}
.title-wrapper {
    width: 100%;
    padding: 10px;
    /* background: #ccc; */
    margin-bottom: 20px;
    background: radial-gradient(ellipse at center, #fff 0%,#f7f7f7 100%);
    /* background: linear-gradient(to right, #4fc08d, #bf5050); */
    border-bottom: 1px solid #ccc;
}
.title {
    text-align: center;
    font-weight: 900;
    margin: 0;
    color: #4fc08d;
}
.title span {
    color: #bf5050;
}
.app-container {
    display: flex;
    justify-content: center;
    flex-flow: column;
    width: 900px;
    margin: 0 auto;
}
.row {
    margin-right: 0;
    margin-left: 0;
}
</style>
