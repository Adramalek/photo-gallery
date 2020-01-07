<template>
  <div>
    <Slider />
    <Photo />
  </div>
</template>

<script>
import Slider from '@/components/Slider.vue';
import Photo from '@/components/Photo.vue';

export default {
  name: 'photo',
  components: {
    Slider,
    Photo,
  },
};
</script>
