<template>
  <div>
    <nav-bar class="home-nav"><template slot="center">购物车</template></nav-bar>
    <home-swiper :banner="banner"></home-swiper>
    <recommend-view :recommend="recommend"></recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="['流行', '新款', '精选']"></tab-control>
  </div>
</template>

<script>
  import homeSwiper from "./childComps/HomeSwiper";
  import RecommendView from "./childComps/RecommendView";
  import FeatureView from "./childComps/FeatureView";


  import NavBar from "components/common/navbar/NavBar";
  import TabControl from "components/content/tabControl/TabControl";
  import {getHomeMultiData} from 'network/home'
export default {
name: "Home",
  components:{NavBar,homeSwiper,RecommendView,FeatureView,TabControl},
  data(){
    return{
      banner:[],
      recommend:[],
      goods:{
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0, list: []},
      },
    }
  },
  mounted() {
  this.getHomeMultiData()
  },
  methods:{
  getHomeMultiData(){
    getHomeMultiData().then(
      (res)=>{
        this.recommend = res.data.recommend.list
        this.banner = res.data.banner.list
      }
    )
  }
  }
}
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: #fff;
  }
</style>