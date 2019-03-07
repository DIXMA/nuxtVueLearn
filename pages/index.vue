<template lang="html">
    <div class="container">
        <h1 class="title">Albums de la pagina</h1>
        <div class="columns is-multiline">
            <albumcard v-for="album in albums" :key="album.id" :album="album" />
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import env from '../config/env';
    import Albumcard from "../components/albumcard";
    export default {
        name: 'IndexPage',
        components: {Albumcard},
        data(){
            return {
                albums: []
            }
        },
        created(){
            axios.get(`${env.endpoint}/albums`).then(response =>{
                this.albums = response.data;
            })
        }
    }
</script>

<style scoped>

</style>