<template>
  <carousel :slides="slides" :controls="true" :indicators="true" :interval="3000" :width="1000" :height="450"></carousel>
</template>

<script>
  import Carousel from './components/carousel/Carousel.vue';

  export default {
    components: {
        Carousel
    },
    data() {
      return {
        slides: [
          'https://picsum.photos/id/234/1000/450',
          'https://picsum.photos/id/235/1000/450',
          'https://picsum.photos/id/236/1000/450',
          'https://picsum.photos/id/237/1000/450',
          'https://picsum.photos/id/238/1000/450'
        ]
      }
    }
  }
</script>

<style lang="scss">

</style>
