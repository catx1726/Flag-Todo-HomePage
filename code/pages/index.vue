<template>
  <main class="index-container">
    Index
  </main>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      title: 'Index'
    }
  },
  head() {
    return { title: this.title }
  }
}
</script>

<style lang="scss" scoped>
.index-container {
  z-index: 10;
  height: 80vh;
  overflow: auto;
}
</style>
