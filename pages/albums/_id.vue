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
        created() {
            let id = this.$route.params.id;
            axios.get(`${env.endpoint}/albums/${id}`).then(response => {
                this.album = response.data;
            });
            axios.get(`${env.endpoint}/albums/${id}/photos`).then(response => {
                this.photos = response.data;
            });
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