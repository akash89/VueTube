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
            let parser = new DOMParser;
            let parsed = parser.parseFromString(this.video.snippet.title, "text/html");
            var desc = parsed.body.innerText;
            
            if (desc.length > 55) {
                desc = desc.slice(0,52) + "...";
            }

            return desc;
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
        margin-bottom: 10px;
        border-radius: 2px;
    }
    li:hover {
        background-color: #eee; 
    }
    li p {
        margin: 0;
        font-size: 0.9em;
        padding: 4px 6px;
    }
</style>

