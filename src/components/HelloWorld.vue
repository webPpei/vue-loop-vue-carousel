<template>
  <div class="loop">
    <div class="left">
      <ul class="imgList" ref="left_container">
        <li v-for="(item, index) in banners" :style="getUrl(item)" :key="index"></li>
      </ul>
    </div>
    <div class="right">
      <ul class="imgList" ref="right_container">
        <li v-for="(item, index) in rightBanners" :style="getUrl(item)" :key="index" :class="{'onlyOne': banners.length <= 1}"></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    banners: {
      type: Array,
      default () {
        return ['https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1531292979&di=30ee440c516d2c8e9643a06b5269fe68&src=http://p18.qhimg.com/bdr/__/d/_open360/fengjing0328/31.jpg']
      }
    }
  },
  data () {
    return {
      currentLoopIndex: 0, // 当前的轮播索引
      li_length: 0, // 图片数组长度
      rightBanners: [], // 右边图片集合
      clientHeight: 0, // 当前client的高度
      flag: true // 当前是顺轮播还是逆轮播
    }
  },
  mounted () {
    // 初始化 init
    this.initLoop()
  },
  beforeDestroy () {
    // 在destory 钩子中 清除定时器
    clearInterval(this.timer)
  },
  methods: {
    getUrl (item) {
      return `background-image: url(${item});height: ${100 / this.li_length}%`
    },
    initLoop () {
      // right 图片需要 倒序
      this.rightBanners = this.banners.slice().reverse()
      if (this.banners.length <= 1) {
        return
      }
      clearInterval(this.timer)
      // 初始化一些数据
      this.li_length = this.banners.length
      // 获取浏览器当前的高度
      this.clientHeight = document.documentElement.clientHeight
      // 根据 banners 的数量 计算 左右 ul 的高度
      let offsetY = this.clientHeight * this.li_length + 'px'
      // 计算右边ul的偏移量
      this.offsetYRNumber = this.clientHeight * (this.li_length - 1)
      this.offsetYR = this.offsetYRNumber + 'px'
      // 设置左右ul的高度
      this.$refs.left_container.style.height = offsetY
      this.$refs.right_container.style.height = offsetY
      this.$refs.right_container.style.transform = `translate3d(-50%, -${this.offsetYR}, 0)`
      this.loop()
    },
    loop () {
      this.timer = setInterval(() => {
        // 顺方向轮播 ++
        if (this.flag) {
          this.currentLoopIndex += 1
          // 对当前轮播的索引进行判断 是否是顺方向轮播
          if (this.currentLoopIndex >= this.li_length - 1) {
            this.flag = false
          }
        } else {
          // 逆方向轮播 --
          this.currentLoopIndex -= 1
          if (this.currentLoopIndex <= 0) {
            this.flag = true
          }
        }
        // 计算左右的偏移量
        const offsetYL = -(this.clientHeight * this.currentLoopIndex) + 'px'
        const offsetY = -(this.offsetYRNumber - (this.clientHeight * this.currentLoopIndex)) + 'px'

        //  设置左右轮播的偏移量 跟 动画
        this.$refs.right_container.style.transform = `translate3d(-50%, ${offsetY}, 0)`
        this.$refs.right_container.style.transition = `all 1.5s cubic-bezier(.35,.52,.11,.8)`
        this.$refs.left_container.style.transform = `translate3d(0, ${offsetYL}, 0)`
        this.$refs.left_container.style.transition = `all 1.5s cubic-bezier(.35,.52,.11,.8)`
      }, 3500)
      // setInterVal 的时间 必须 大于 transition 的时间
    }
  }
}
</script>

<style scoped lang="less">
.loop {
  box-sizing: border-box;
  height: 100%;
  width: 100%;
  position: absolute;
  overflow: hidden;
  max-width: 1920px;
  max-height: 1080px;
  background-size: cover;
  .left {
    width: 100%;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    z-index: 1;
    height: 100%;
    .imgList {
      width: 100%;
      height: 100%;
      li {
        background-size: cover;
        background-position: 50% 50%;
        height: 25%;
        width: 100%;

      }
    }
    span{
      width: 155px;
      height: 53px;
      display: inline-block;
      background-color: #ffffff;
      font-family: AdobeHeitiStd-Regular;
      font-size: 16px;
      line-height: 53px;
      text-align: center;
      position: fixed;
      left: 0;
      top: 5%;
      z-index: 99999;
    }
  }
  .right {
    position: absolute;
    right: -50%;
    bottom: 0;
    width: 100%;
    height: 100%;
    z-index: 2;
    overflow:hidden;
    .imgList {
      width: 100%;
      height: 100%;
      li {
        width: 100%;
        height: 25%;
        overflow: hidden;
        -webkit-background-size: cover;
        background-size: cover;
        background-position: 50% 50%;
        &.onlyOne {
          transform: translateX(-50%)
        }
      }
    }
  }
}
</style>
