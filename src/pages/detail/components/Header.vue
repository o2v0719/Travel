<template>
  <div>
    <router-link tag="div" to="/" class="header-abs" v-show="showAbs">
      <span class="iconfont iconarrow-left-bold header-abs-back"></span>
    </router-link>
    <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
      <div class="iconfont iconarrow-left-bold header-fixed-back"></div>
      景点详情
    </div>
  </div>
</template>

<script>

export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  // activated () {
  mounted () {
    // scroll事件发生，就会执行handleScroll事件
    // 注意此处的window为全局对象
    window.addEventListener('scroll', this.handleScroll)
  },
  // deactivated () {
  destroyed () {
    // 给全局window解绑：当离开当前页面时，不再触发scroll事件
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop || document.body.scrollTop || window.pageYOffset
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = {
          opacity
        }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  }

}
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header-abs
  position absolute
  left 0.2rem
  top 0.2rem
  width 0.8rem
  height 0.8rem
  border-radius 0.4rem
  text-align center
  line-height 0.8rem
  background rgba(0, 0, 0, 0.8)
  .header-abs-back
    color #fff
    font-size 0.4rem
.header-fixed
  z-index 2
  position fixed
  top 0
  left 0
  right 0
  height $headerHeight
  line-height $headerHeight
  text-align center
  color #fff
  background $bgColor
  font-size 0.32rem
  .header-fixed-back
    position absolute
    top 0
    left 0
    width 0.64rem
    text-align center
    font-size 0.4rem
    color #fff
</style>