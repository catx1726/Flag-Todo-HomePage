<template>
  <div class="header-container">
    <ul class="link-container">
      <li v-for="item in navList" :key="item.link" class="link-item large-slim">
        <a :href="item.link">{{ item.text }}</a>
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
  height: 10vh;
  display: flex;
  justify-content: flex-end;
  align-items: center;
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
}
</style>
