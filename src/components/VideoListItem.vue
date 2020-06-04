<template>
    <li class="list-group-item media" @click="onVideoSelect">
        <img :src="thumbnailUrl"/>
        <p class="media-body">{{ title }}</p> 
    </li>
</template>

<script>
export default {
    name: 'VideoListItem',
    props: ['video'],
    computed: {
        thumbnailUrl() {
            return this.video.snippet.thumbnails.default.url;
        },
        title() {
            var parser = new DOMParser;
            return parser.parseFromString(this.video.snippet.title, 'text/html');
        }
    },
    methods: {
        onVideoSelect() {
            this.$emit('videoSelect', this.video);
        }
    }  
};
</script>

<style scoped>
    li {
        display: flex;
        cursor: pointer;
        padding: 0;
        /* flex-flow: column wrap; */
    }
    li:hover {
        background-color: #eee; 
    }
    li p {
        margin: 0;
        font-size: 0.9em;
    }
</style>

