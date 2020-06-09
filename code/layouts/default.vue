<template>
  <v-app class="html-container" :style="{ backgroundImage: 'url:(' + bgImg + ')' }">
    <MyHeader />
    <Nuxt class="content-container" />
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
      bgImg: ''
    }
  },

  watch: {
    bgImg(val) {
      console.log('watch bgImg:', val)
    }
  },
  created() {
    this.fetchBGImg()
  },
  methods: {
    async fetchBGImg() {
      try {
        const res = await this.$axios.$get('/bing/HPImageArchive.aspx?format=js&idx=0&n=1')
        this.bgImg = 'https://cn.bing.com' + res.images[0].url
        console.log('fetchBGImg res:', this.bgImg)
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.html-container {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
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
</style>
