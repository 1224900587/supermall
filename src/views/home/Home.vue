<template>
  <div id="home">
    <nav-bar class="home-nav">
      <span slot="center">购物街</span>
    </nav-bar>
    <recommend-view :recommends='recommends' />
    <feature-view />
    <tab-control :titles='["流行","新款","精选"]' @cilckcon='cilckcon' />
    <goods-list :goods="showGoods" />
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/Navbar'
import RecommendView from 'views/home/childComps/RecommendView'
import FeatureView from './childComps/featureView'
import TabControl from 'components/content/tabcontrol/tabcontrol'
import GoodsList from 'components/content/goods/goodsList'

import { getHomeMultidata } from 'network/home'
import { getHomeGoods } from 'network/home'

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
      currentType:"pop"
    }
  },
  components: {
    NavBar,
    RecommendView,
    FeatureView,
    TabControl,
    GoodsList
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
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  text-align: center;
}
</style>
