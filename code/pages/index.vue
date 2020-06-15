<template>
  <main class="index-container">
    <div class="workspace-container ft-2">
      <div class="show-trigger">
        <v-icon color="white" @click="showFlageAndTodo()">
          {{ lockTandF ? 'mdi-arrow-expand-left' : 'mdi-arrow-expand-right' }}
        </v-icon>
      </div>
      <div ref="flag" class="flag-container ">Flag</div>
      <div ref="todo" class="todo-container ">Todo</div>
    </div>

    <div class="search-container m-flex flex-jc-center flex-an-center ft-2 ft-wt-light">
      <label>搜索:</label>
      <input v-model="keywords" type="text" autofocus @ @keyup.enter="search" />
      <v-icon class="search-icon" @click="search(keywords)">
        mdi-magnify
      </v-icon>
    </div>
  </main>
</template>

<script>
export default {
  name: 'Index',
  components: {},
  props: { bgCopyright: { type: String, default: '' } },
  data() {
    return {
      keywords: '',
      lockTandF: false, // DES 控制 flag 和 todo
      title: 'Index'
    }
  },
  mounted() {
    console.log('parent bgCopryright:', this.bgCopryright)
  },
  methods: {
    showFlageAndTodo() {
      if (this.lockTandF) {
        this.$refs.todo.classList.remove('show')
        this.$refs.flag.classList.remove('show')
        this.lockTandF = !this.lockTandF
        return
      }
      this.lockTandF = !this.lockTandF
      this.$refs.todo.classList.add('show')
      this.$refs.flag.classList.add('show')
    },
    search(event) {
      if (!this.keywords && event.keyCode !== 13) {
        return
      }
      window.open('https://cn.bing.com/search?q=' + this.keywords)
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
  height: 100vh;
}
.search-container {
  left: 0;
  bottom: 100px;
  z-index: 99;
  position: fixed;
  .search-icon {
    opacity: 0;
    font-size: 2rem;
    cursor: pointer;
    transform: scale(0);
    transition: all 0.3s ease;
  }
  label {
    width: 5rem;
  }
  input {
    width: 16rem;
    outline: transparent;
    border-bottom: white solid 1px;
  }
  put:focus ~ .search-icon {
    opacity: 1;
    color: white;
    transform: scale(1);
  }
}

.workspace-container {
  left: 0;
  top: 0;
  user-select: none;
  position: absolute;
  .show-trigger {
    color: white;
    cursor: pointer;
  }
  .todo,
  .flag {
    &-container {
      transform: translateX(-500px);
      transition: all 0.3s ease;
    }
  }
  .todo-container {
    top: 15%;
  }
  .flag-container {
    top: 30%;
  }
}
.show {
  transform: translateX(0) !important;
}
.trigger-show {
  transform: translateX(20px);
}
</style>
