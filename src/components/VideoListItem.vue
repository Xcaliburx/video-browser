<template>
    <li class="list-group-item" @click="onVideoSelect">
        <!-- <img :src="video.snippet.thumbnails.default.url" alt=""/> -->
        <img :src="thumbnailUrl" alt=""/>
        <div>
            {{ video.snippet.title }}
        </div>
    </li>
</template>

<script>
export default {
    name: 'VideoListItem',
    props: ['video'],
    computed: {
        thumbnailUrl() {
            return this.video.snippet.thumbnails.default.url;
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
        flex-direction: row;
        cursor: pointer;
    }

    li:hover {
        background-color: #eee;
    }

    div {
        margin-left: 20px;
    }
</style>