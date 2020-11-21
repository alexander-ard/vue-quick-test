<template>
  <div class="thumbnail">
    <img :src="thumbUrl"/>
  </div>
</template>

<script>
export default {
  name: "thumbnail",
  props: ["url", "id"],
  computed: {
      thumbUrl() {
          return this.url;
      }
  }
};
</script>

<style>
    .thumbnail {
        display: flex;
    }

/*
Border 1 border: Green.
Border 2 border: Blue.
Albúm 3 border: Purple.
*/
</style>
