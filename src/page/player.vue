<style lang="scss" scoped>
@import './../style/mixin.scss';
.router-up-enter-active, .router-up-leave-active {
    transition: all .4s;
    opacity:0;
}
.router-up-enter, .router-up-leave-active {
    transform: translate3d(0, 100%, 0);
    opacity:1;
}
section{
	padding-top:0.4rem;
	padding-bottom:0.3rem;
	.weui-cell__hd{
		padding-right:.1rem;
	}
}
.weui-btn{
	border-radius:.2rem;
	margin:0 .1rem;
}
</style>
<template>
  <transition name="router-up" mode="out-in">
    <div>
      <div class="blur-background" :style="playInfo&&'background-image:url('+playInfo.album.picUrl+')'">
        <div class="weui-mask"></div>
      </div>
      <music-header :title="playInfo.name" :desc="playInfo.artists | artists" :contain="{share:true,back:true}" class="transparent-nav"></music-header>
      <audio :src="mp3Url"></audio>
    </div>
  </transition>
</template>
<script>
import {mapMutations,mapState} from 'vuex'
import musicHeader from '../components/music-header.vue'
import fetch from '../config/fetch'
export default {
  components:{
    musicHeader
  },
  data () {
    return {
      mp3Url:null
    }
  },
  computed:{
    ...mapState([
      'playInfo'
    ])
  },
  watch:{
    playInfo:function(val){
      if(val){
        this.playInfo = val;
      }
    }
  },
  created(){
    // this.mp3Url = getMp3Url(this.playInfo.id);
  },
  filters: {

  },
  methods:{
  	...mapMutations([
  	    'INIT_PLAYINFO',
  	]),
    // async getMp3Url(id){
    //   let re  = await fetch('GET','/api/song/enhance/player/url',{ids:[id]});
    //   return re;
    // }
  }
}
</script>