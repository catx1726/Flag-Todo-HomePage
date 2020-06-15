<template>
  <v-app ref="html-container" class="html-container">
    <div class="img-preload">
      <img :src="bgImg.src" />
    </div>
    <div class="copyright-container">
      <a :href="'https://cn.bing.com/search?q=' + bgImg.copyright" target="_blank">
        {{ bgImg.copyright }}
      </a>
    </div>
    <transition name="content">
      <Nuxt class="content-container" />
    </transition>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      bgImg: {
        src:
          'https://github.com/catx1726/Bing-Img-Repo/blob/master/imgs/bing/2020/06/OHR.LionSurfing_ZH-CN7369892268.jpg',
        copyright: 'test'
      }
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
        this.bgImg.src = 'https://cn.bing.com' + res.images[0].url
        this.bgImg.copyright = res.images[0].copyright
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
  height: 100vh;
  font-size: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  color: white;
}
.copyright-container {
  z-index: 99;
  width: 20rem;
  padding: 5px 20px;
  bottom: 0;
  color: white;
  font-size: 16px;
  font-weight: 100;
  position: fixed;
  background-color: #00000085;
  a {
    color: white;
    text-decoration: none;
  }
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
