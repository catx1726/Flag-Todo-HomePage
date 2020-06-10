<template>
  <div class="header-container">
    <ul class="link-container">
      <li v-for="item in navList" :key="item.link" class="link-item large-slim">
        <NuxtLink :to="item.link">{{ item.text }}</NuxtLink>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
  name: 'MyHeader',

  components: {},
  data() {
    return {
      navList: []
    }
  },

  computed: {},

  watch: {},

  beforeMount() {},

  mounted() {},

  created() {
    this.navList = this.getNavList()
  },
  methods: {
    ...mapGetters({
      getNavList: 'header/getAllNavList'
    })
  }
}
</script>
<style lang="scss" scoped>
.header-container {
  z-index: 10;
  height: 10vh;
  display: flex;
  justify-content: flex-end;
  align-items: center;
  @media screen and (max-width: 800px) {
    height: 5vh;
  }
}
.link-container {
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  list-style: none;
  background-color: white;
  .link-item {
    min-width: 50px;
    width: 5vw;
    a {
      color: black;
      text-decoration: none;
      transition: all 0.3s ease;
    }
    a:hover {
      color: rgba($color: pink, $alpha: 1);
    }
  }
}
.large-slim {
  font-size: 24px;
  font-weight: 100;
  @media screen and (max-width: 800px) {
    font-size: 16px;
  }
}
</style>
