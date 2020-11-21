<template>
    <div class="album" :style="albumColor">
        <span class="album__id">
            Album: {{ album.id }}
            <div class="album__thumbnails">
                <div v-for="thumb in album.pictures" :key="thumb.id">
                    <thumbnail :url="thumb.thumb" :id="thumb.id"/>
                    <a target="__blank" :href="thumb.url">View</a>
                </div>
            </div>
        </span>
    </div>
</template>

<script>
import Thumbnail from './Thumbnail.vue';

export default {
    name: 'album',
    props: ['album'],
    components: { Thumbnail },
    data() {
        return {

        }
    },
    beforeMount() {
        console.log(this.album);
    },
    computed: {
        albumColor() {
            return `border: 3px solid ${this.album.color}`;
        }
    }
}
</script>

<style scoped>

 .album {
     display: flex;
     flex-direction: column;
 }

    .album__id {
        font-size: 2em;
    }

 .album__thumbnails {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
 }  

</style>