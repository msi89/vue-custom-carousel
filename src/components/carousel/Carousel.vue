<template>
   <div class="carousel">
       <div class="slider">
           <slot></slot>
       </div>
        <div class="nav">
            <button @click.prevent="prev" v-show="nav" class="btn-nav">&#60;</button>
            <button @click.prevent="next" v-show="nav" class="btn-nav">&#62;</button>
        </div>
        <div class="banner" :class="{frame:frame}" v-show="banner">
            <button v-for="(slide,i) in slides" :key="i" 
               class="dot" @click.prevent="goto(i)" :class="{active: i == index }">
            </button>
        </div>
    </div>
</template>

<script>
import { Stream } from 'stream';
import { clearInterval } from 'timers';
export default {
    props:{
        banner: {type: Boolean, default: true},
        nav: {type: Boolean, default: true},
        autoplay: {type: Boolean, default: true},
        frame: {type: Boolean, default: true},
        interval: {type: Number, default: 5000},
    },
    data(){
        return {
            index: 0,
            slides: [],
            direction: 'right'
        }
    },
    computed: {
        slideCount() { return this.slides.length }
    },
    methods: {
        next () {
            this.index ++
            this.direction = 'right'
            if(this.index >= this.slideCount ){
                this.index = 0
            }
        },
        prev () {
            this.index --
            this.direction = 'left'
            if(this.index < 0){
                this.index = this.slideCount - 1
            }
        },
        goto(index) {
            this.direction = index > this.index ? 'right' : 'left'
            this.index = index
        },
        play(){
           var timerId= setInterval(() => {
              this.next ()
            }, this.interval);
        }
    },
    mounted(){
        this.slides = this.$children
        // this.slides.forEach((slide, i) =>{
        //     slide.index = i
        // })
        if(this.autoplay){
            this.play()
        }
    },
    destroyed(){
        clearInterval(timerId)
    }
}
</script>


<style  lang="scss">
.carousel{
  position: relative;
  overflow: hidden;
  height: 500px;

  .slider{
    position: absolute;
    width: 100%;
    height: 100%;
  }
  .banner{
    position: absolute;
    width: 100%;
    padding: 10px;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 2;
    .dot{
        border:0;
        width: 10px;
        height: 10px;
        border-radius: 10px;
        background: rgba(0, 0, 0, 0.6);
        margin: 3px;
        outline: none;
    }
    .dot:focus{
        border: 1px solid coral;
    }
    .dot.active{
        background: coral;
    }
    
  }
  .banner.frame{
        background: rgba(0, 0, 0, 0.6);
   }
  .nav {
    position: absolute;
    display: flex;
    width: 100%;
    height: 100%;
    justify-content: space-between;
    align-items: center;
    background: transparent;
    z-index: 1;
    .btn-nav{
        font-weight: bold;
        font-size: 16px;
        color: #fff;
        width: 45px;
        height: 45px;
        border: 0;
        margin: 10px;
        border-radius: 45px;
        outline: none;
        background: rgba(0, 0, 0, 0.6)
    }
  }
}


</style>
