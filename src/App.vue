<!-- en remplaçant les slot par le code
<carousel>
    <div class="carousel">
      <carousel-slide v-for="n in slides" :key= "n" :index="n-1" >
        <transition :name="transition">
        <div v-show="visible">
          <div style="position:absolute;left:0;right:0;text-align:center;top:40%;color:#FFF;font-size:16px;">Slide {{n}} </div>
          <img :src="'https://picsum.photos/630/300/?image=' + n" width="100%">
      </carousel-slide>
    <button class="carousel__nav carousel__prev" @click.prevent="previous">Préc</button>
    <button class="carousel__nav carousel__next" @click.prevent="next">Suiv</button>
    <div class="carousel__pagination">
      <button v-for="n in slidesCount" :key="n" @click="goto(n-1)" :class="{active: n-1 == index}"></button>
    </div>
</carousel>
-->  
<template>
  <div id="app">
    <carousel>
      <carousel-slide v-for="n in slides" :key="n" :index="n-1">
        <div
          style="position:absolute;left:0;right:0;text-align:center;top:40%;color:#FFF;font-size:16px;"
        >Slide {{n}}</div>
        <img :src="'https://picsum.photos/630/300/?image=' + n" width="100%">
      </carousel-slide>
    </carousel>
    <button @click="addSlide">+</button>
    <button @click="removeSlide">-</button>
  </div>
</template>

<script>
import Carousel from "./components/carousel/Carousel";
import CarouselSlide from "./components/carousel/CarouselSlide";

export default {
  data() {
    return {
      slides: 5,
      n: 1
    };
  },
  methods: {
    addSlide() {
      this.slides++;
    },
    removeSlide() {
      this.slides--;
    }
  },
  name: "App",
  components: {
    Carousel,
    CarouselSlide
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  color: #c9161680;
  /* margin-top: 60px;*/
}
</style>
