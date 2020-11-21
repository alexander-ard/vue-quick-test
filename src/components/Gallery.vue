<template>
  
    <div class="albums">
        <div class="album" v-for="album in albums" :key="album.id">
            <album :album="album"/>
        </div>
    </div>

</template>

<script>
import Album from './Album.vue';

export default {
  components: { Album },
    name: 'gallery',
    data() {
        return {
            albums: [],
            colors: ['green','blue','purple']
        }
    },
    beforeMount(){
        this.getAlbums();
        console.log(this.albums);
    },
    methods:{
        getAlbums: function() {
            fetch('https://jsonplaceholder.typicode.com/photos')
            .then(response => response.json())
            .then((resp) => {
                const maxAlbums = Math.max(...resp.map(x => { return x.albumId }));
                const filtered = resp.filter(x => { return x.albumId > maxAlbums - 3 });
                const ids = Array.from(new Set(filtered.map(x => { return x.albumId})));

                ids.forEach(i => {
                    const photos = filtered
                                    .filter(f => {
                                        return f.albumId == i
                                    })
                                    .map(f => {
                                        return {
                                            id: f.id,
                                            title: f.title,
                                            thumb: f.thumbnailUrl,
                                            url: f.url
                                        }
                                    });
                    
                    const max = Math.max(...photos.map(x => { return x.id }));

                    this.albums.push(
                        {
                            id: i,
                            pictures: photos.filter(x => { return x.id > max -2 }),
                            color: this.colors[maxAlbums - i]
                        }
                    )
                });
                
            });
        }
    }
}
</script>

<style>
    .albums {
        display: grid;
    }

    .album {
        padding: 1em;
    }

</style>