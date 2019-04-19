<template>
  <div class="carousel">
    <slot></slot>
    <button class="carousel__nav carousel__prev" @click.prevent="previous">Préc</button>
    <button class="carousel__nav carousel__next" @click.prevent="next">Suiv</button>
    <div class="carousel__pagination">
      <button v-for="n in slidesCount" :key="n" @click="goto(n-1)" :class="{active: n-1 == index}"></button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      index: 0,
      slides: [],
      direction: 'right'
    };
  },
  watch:{
    slides(slides) {
      if (this.index >= this.slidesCount) {
         this.index = this.slidesCount - 1 }
    }
  },
  computed: {
    slidesCount() {
      return this.slides.length;
    }
  },
  methods: {
    goto(index) {
      this.direction = index > this.index ? "right" : "left";
      this.index = index;
    },
    next() {
      if (this.index >= this.slidesCount - 1) {
        this.index = 0;
      } else {
        this.index += 1;
      }
      this.direction = "right";
    },
    previous() {
      if (this.index == 0) {
        this.index = this.slidesCount - 1;
      } else {
        this.index -= 1;
      }
      this.direction = "left";
    }
  },
  mounted() {
    this.slides = this.$children;
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.carousel {
  position: relative;
  overflow: hidden;
}
.carousel__nav {
  position: absolute;
  margin-top: -31px;
  top: 40%;
  left: 10px;
  width: 63px;
  height: 63px;
}
.carousel__nav.carousel__next {
  right: 10px;
  left: auto;
}
.carousel__pagination {
  position: absolute;
  bottom: 10px;
  left: 0;
  right: 0;
  text-align: center;
}
.carousel__pagination button {
  display: inline-block;
  width: 15px;
  height: 15px;
  background-color: #000;
  opacity: 0.8;
  border-radius: 15px;
  margin: 0 2px;
}
.carousel__pagination button.active {
  background-color: #FFF;
}
</style>
