<template lang="html">
    <div class="container">
        <nuxt-link to="/">back</nuxt-link>
        <h1 class="title">{{ album.title }}</h1>
        <div class="columns is-multiline">
            <div class="column is-one-quarter" v-for="photo in photos" :key="photo.id">
                <img :src="photo.url" :alt="photo.title">
            </div>
        </div>
    </div>
</template>

<script>
    import router from 'vue-router';
    import axios from 'axios';
    import env from '../../config/env';
    export default {
        name: 'AlbumIndvPage',
        data(){
            return {
                album: {},
                photos: []
            }
        },
        created: async function(){
            let id = this.$route.params.id;
            let albumResponse = await axios.get(`${env.endpoint}/albums/${id}`);
            this.album = albumResponse.data;
            let photoResponse = await axios.get(`${env.endpoint}/albums/${id}/photos`);
            this.photos = photoResponse.data;
        }
    }
</script>

<style scoped>
    .title{
        margin-top: 100px;
    }
    .container{
        text-align: center;
    }
</style>