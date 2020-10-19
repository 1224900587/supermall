<template>
  <div id="home">
    <nav-bar class="home-nav">
      <span slot="center">购物街</span>
    </nav-bar>
    <scroll class="contents" ref="backTop" :probe-type='3' @scroll='contentScroll' :pull-up-load='true' @pullingup='pullup'>
      <recommend-view :recommends='recommends' />
      <feature-view />
      <tab-control :titles='["流行","新款","精选"]' @cilckcon='cilckcon' />
      <goods-list :goods="showGoods" />
    </scroll>
    <back-top @click.native='clickBacktop' v-show='showBackTop' />
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/Navbar'
import RecommendView from 'views/home/childComps/RecommendView'
import FeatureView from './childComps/featureView'
import TabControl from 'components/content/tabcontrol/tabcontrol'
import GoodsList from 'components/content/goods/goodsList'
import BackTop from 'components/content/backtop/backTop'

import { getHomeMultidata } from 'network/home'
import { getHomeGoods } from 'network/home'

import Scroll from 'components/content/scroll/scroll'

export default {
  name: 'home',
  data() {
    return {
      banners: [],
      recommends: [],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]}
      },
      currentType:"pop",
      showBackTop:false
    }
  },
  components: {
    NavBar,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
  },
  created() {
    this.getHomeMultidata();
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  methods:{
    // 网络请求
    getHomeMultidata(){
        getHomeMultidata().then((res) => {
        this.banners = res.data.banner
        this.recommends = res.data.recommend.list
    })
    },
    getHomeGoods(type){
        const page=this.goods[type].page+1;
        getHomeGoods(type,page).then((res)=>{
        this.goods[type].list.push(...res.data.list)
        this.$refs.backTop.finishPullUps()
    })
    // 事件监听
    },
    cilckcon(index){
        switch (index) {
            case 0:
                this.currentType='pop'
                break;
            case 1:
                this.currentType='new'
                break;
            case 2:
                this.currentType='sell'
                break;
        }
    },
    clickBacktop(){
      this.$refs.backTop.scrollTo(0,0,500)
    },
    contentScroll(position){
      position.y<-1000?this.showBackTop=true:this.showBackTop=false
    },
    pullup(){
      this.getHomeGoods(this.currentType)
    }
  },
  computed:{
      showGoods(){
         return this.goods[this.currentType].list
      }
  }
}
</script>

<style scoped>
#home {
    /*padding-top: 44px;*/
    height: 100vh;
    position: relative;
  }

.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  text-align: center;
}

.contents{
    overflow: hidden;
  /* height: calc(100vh - 93px); */
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
}
</style>
