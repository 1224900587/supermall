<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BetterScroll from 'better-scroll'

export default {
  props:{
    probeType:{
      type:Number,
      default:0
    },
    pullUpLoad:{
      type:Boolean,
      default:false
    }
  },
  data () {
    return {
      scroll:null
    };
  },
  mounted(){
    setTimeout(() => {
      this.scroll=new BetterScroll(this.$refs.wrapper,{
      click:true,
      probeType:this.probeType,
      pullUpLoad: this.pullUpLoad,
      })
      this.scroll.on('scroll',position=>{
        this.$emit('scroll',position)
      })
      this.scroll.on('pullingUp',()=>{
        this.$emit('pullingup')
      })
    }, 1000);
  },
  methods:{
    scrollTo(x,y,time=500){
      this.scroll.scrollTo(x,y,time)
    },
    finishPullUps(){
      this.scroll.finishPullUp();
    }
  }
}

</script>
<style lang='scss' scoped>
</style>
