<template>
  <v-app ref="html-container" class="html-container">
    <div class="img-preload">
      <img :src="bgImg" />
    </div>
    <MyHeader />
    <transition name="content">
      <Nuxt class="content-container" />
    </transition>
    <MyFooter />
  </v-app>
</template>

<script>
import MyHeader from '~/components/MyHeader'
import MyFooter from '~/components/MyFooter'

export default {
  components: {
    MyHeader,
    MyFooter
  },
  data() {
    return {
      bgImg:
        'https://github.com/catx1726/Bing-Img-Repo/blob/master/imgs/bing/2020/06/OHR.LionSurfing_ZH-CN7369892268.jpg'
    }
  },

  watch: {
    bgImg(val) {
      console.log('watch bgImg:', val)
    }
  },
  mounted() {},
  created() {
    this.fetchBGImg()
  },
  methods: {
    async fetchBGImg() {
      try {
        const res = await this.$axios.$get('/bing/HPImageArchive.aspx?format=js&idx=0&n=1')
        this.bgImg = 'https://cn.bing.com' + res.images[0].url
        // console.log('fetchBGImg res:', this.bgImg, this.$refs['html-container'])
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.html-container {
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  position: relative;
  // background-image: url('/imgs/TV-80 玲.png');
}
.content-container {
  height: 80vh;
  font-size: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  color: white;
}
.img-preload {
  z-index: 1;
  img {
    height: 100vh;
    width: 100vw;
    object-fit: cover;
  }
  height: 100vh;
  overflow: hidden;
  position: absolute;
}
// content page transition
.content-enter-active,
.content-leave-active {
  transition: opacity 0.3s ease;
}
.content-enter, .content-leave-to
/* .component-fade-leave-active for below version 2.1.8 */ {
  opacity: 0;
}
</style>
