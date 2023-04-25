<template>
  <div class="home">
    <Carousel :options="options" />
  </div>
</template>

<script>
// @ is an alias to /src
import Carousel from "@/components/Carousel.vue";

export default {
  name: "Home",
  components: {
    Carousel,
  },
  data() {
    return {
      options: {
        imgs: [
          "https://plus.unsplash.com/premium_photo-1677234147673-fad786a3e2f1",
          "https://images.unsplash.com/photo-1682250134515-da20e2e9a6db",
          "https://images.unsplash.com/photo-1682249301375-5c7f5a286d8c",
        ],
      },
    };
  },
  mounted() {},
  methods: {},
};
</script>
