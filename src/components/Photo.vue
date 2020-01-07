<template>
  <div class="lightbox" @click.self="closeLightbox">
    <img v-if="photo.id > 1" class="rotate" :src="photoUrl(photo.filename)" alt="">
    <img v-if="photo.id <= 1" :src="photoUrl(photo.filename)" alt="">
    <div class="lightbox-info">
      <div class="lightbox-info-inner">
        <p v-if="photo.memory">{{photo.memory}}</p>
      </div>
    </div>
  </div>
</template>

<script>
import photos from '@/photos.json';

export default {
  name: 'Photo',
  data() {
    return {
      photos,
    };
  },
  computed: {
    photo() {
      return this.photos.find(photo => photo.id === Number(this.$route.params.id));
    },
  },
  methods: {
    photoUrl(filename) {
      return require(`../assets/images/${filename}`);
    },
    closeLightbox() {
      this.$router.push('/');
    },
  },
};
</script>

<style>
  .lightbox {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.8);
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 2rem;
  }

  .lightbox img {
    margin: auto;
    width: 100%;
    grid-column-start: 2;
  }

  .lightbox-info {
    margin: auto 2rem auto 0;
  }

  .lightbox-info-inner {
    background-color: #FFFFFF;
    display: inline-block;
    padding: 2rem;
  }

  .rotate {
    transform-origin: center;
    transform: rotate(90deg);
  }
</style>
