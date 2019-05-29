<template>
   <transition :name="transition">
        <div class="slide" v-show="visible">
          <slot></slot>
        </div>
   </transition>
</template>

<script>
export default {
    props: { 
        index: {type: Number, default: 0} 
    },
    computed: {
        visible () { return this.index === this.$parent.index },
        transition () { 
            if(this.$parent.direction){
                return 'slide-'+this.$parent.direction
            }
            //return 'fade'
        }
    }
}
</script>

<style lang="scss">
$duration : 2s;
$fadeDuration : 0.3s;
.slide img{
    width: 100%;
}
.slide-right-enter-active{
    animation: slideRightIn $duration;
}
.slide-right-leave-active{
    animation: slideRightOut $duration;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    width: 100%;
}


.slide-left-enter-active{
    animation: slideLeftIn $duration;
}
.slide-left-leave-active{
    animation: slideLeftOut $duration;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    width: 100%;
}

.fade-enter-active{
    animation: fadeOut $fadeDuration;
}
.fade-leave-active{
    animation: fadeOut $fadeDuration;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    width: 100%;
}
/* slide animations */
@keyframes slideRightIn {
    from{transform: translateX(100%)}
    to{transform: translateX(0)}
}
@keyframes slideRightOut {
    from{transform: translateX(0)}
    to{transform: translateX(-100%)}
}
@keyframes slideLeftIn {
    from{transform: translateX(-100%)}
    to{transform: translateX(0)}
}
@keyframes slideLeftOut {
    from{transform: translateX(0)}
    to{transform: translateX(100%)}
}

/* fade animations */
@keyframes fadeIn {
    from{opacity: 0;}
    to{opacity: 1;}
}
@keyframes fadeOut {
    from{opacity: 1;}
    to{opacity: 0;}
}
</style>
