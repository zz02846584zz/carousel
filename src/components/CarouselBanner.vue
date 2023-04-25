<template>
  <div>
    <div ref="container" class="carousel__container">
      <div ref="list" class="carousel__list">
        <div
          class="carousel__item"
          v-for="(img, index) in options.imgs"
          :key="img + index"
        >
          <img :src="img" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Hammer from "hammerjs";

export default {
  name: "CarouselBanner",
  props: {
    imgs: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
  emits: ["change"],
  data() {
    return {
      itemsTransform: null,
      active: 0,
      imgsData: null,
      frame: null,
      pan: {
        origin: 0,
        diff: 0,
      },
    };
  },
  mounted() {
    this.setData();
    this.$nextTick(() => {
      this.init();
      this.setHammer();
    });
  },
  methods: {
    init() {
      if (!this.options.imgs.length) return;
      const carouselList = this.$refs.list;
      const carouselItems = Array.from(carouselList.children);
      carouselItems.forEach((carouselItem) => {
        carouselList.appendChild(carouselItem.cloneNode(true));
      });

      setTransform();
    },
    setData() {
      this.imgs = this.options.imgs ?? [];
      this.imgsData = this.options.imgs ?? [];
      this.setTransform();
    },
    goSlide() {
      console.log("go slide: " + this.active);
      this.$emit("change", this.active);
    },
    // Hammer
    setHammer() {
      const mc = new Hammer(this.$refs.container, { preventDefault: true });
      mc.add(new Hammer.Pinch({ threshold: 0 }));
      mc.on("panstart", this.onPanStart)
        .on("panmove", this.onPanMove)
        .on("panend", this.onPanEnd);
    },
    onPanStart(e) {
      this.pan.origin = e.center.x;
    },
    onPanMove(e) {
      this.pan.diff = e.center.x - this.pan.origin;
    },
    onPanEnd() {
      this.pan.origin = 0;
      this.pan.diff = 0;
      this.goSlide();
    },
  },
};
</script>

<style scoped lang="scss">
.carousel {
  &__container {
    position: relative;
    width: 100%;
    height: 220px;
    background: #eaeaea;
  }
  &__list {
    display: flex;
    align-items: center;
    gap: 30px;
    height: 300px;
    position: absolute;
  }
  &__item {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 300px;
    height: 130px;
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      pointer-events: none;
    }
  }
}
</style>
