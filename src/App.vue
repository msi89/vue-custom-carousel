<template>
  <div id="app">
    <carousel >
      <slide v-for="s in slides" :key="s" :index="s-1" >
        <div class="carousel-text">
          <h1>Slide {{s}}</h1>
          <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book</p>
        </div> 
        <img :src="`https://picsum.photos/id/${s}/1230/500`" alt="">
      </slide>
    </carousel>
  </div>
</template>

<script>

import Carousel from '@/components/carousel/Carousel'
import Slide from '@/components/carousel/Slide'
export default {
  name: 'app',
  components: {Carousel, Slide},
  data(){
    return {
      slides: 6
    }
  }
}
</script>

<style lang="scss">

*,*::before, *::after{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
.carousel-text{
  position:absolute; 
  width: 300px;
  top: 50px;
  right:10px; 
  color:#fff; 
  text-align:center; 
  p{
    text-align: justify;
  }
}

</style>
