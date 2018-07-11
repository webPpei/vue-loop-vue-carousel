<template>
  <div id="app">
    <HelloWorld :banners="banners"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  data () {
    return {
      banners: [
        'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1531307153141&di=e455169898124b8e609ba0085457f8d3&imgtype=0&src=http%3A%2F%2Fbbsfiles.vivo.com.cn%2Fvivobbs%2Fattachment%2Fforum%2F201601%2F06%2F113530v72cp7ghsa2h2t7t.jpg',
        'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1531305634328&di=d0a02de46bd746e55bfeeb6aa5a214f7&imgtype=0&src=http%3A%2F%2Fimg3.iqilu.com%2Fdata%2Fattachment%2Fforum%2F201308%2F21%2F175426urqebb9946bwb4qe.jpg',
        'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1531305634329&di=86594482c55ced144d0e91c06e7d5de0&imgtype=0&src=http%3A%2F%2Fpic1.win4000.com%2Fwallpaper%2F2017-11-27%2F5a1b830d517c7.jpg',
        'https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1531305634328&di=8eacea286e36c0d3950b40dfb128ac51&imgtype=0&src=http%3A%2F%2Fattach.bbs.miui.com%2Fforum%2F201507%2F30%2F145129fuh3i2bi58bm2cp8.jpg'
      ]
    }
  },
  components: {
    HelloWorld
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>
