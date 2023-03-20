<template>
  <!-- 让所有的item都展示同一个图片和文字样式 -->
  <div class="tab-bar-item" @click="itemClick">
    <div v-if="!isActive">
      <slot name="item-icon">测试1</slot>
    </div>

    <div v-else>
      <slot name="item-icon-active">测试3</slot>
    </div>

    <div :style="activestyle">
      <slot name="item-text">测试2</slot>
    </div>

  </div>
</template>

<script>
export default {
  name: 'TabBarItem',
  props: {
    path: String,
    activeColor: {
      type: String,
      default: 'red'
    }
  },
  data() {
    return {
      // isActive: true
    }
  },
  computed: {
    isActive() {
      // return this.$route.path.indexOf(this.path) !== -1
      if (this.$route.path == this.path) {
        return true
      }
    },
    activestyle() {
      return this.isActive ? { color: this.activeColor } : {}
    }
  },
  methods: {
    itemClick() {
      // console.log('this.itemClick');
      this.$router.replace(this.path)
      console.log(this.path);
    }
  },
}
</script>

<style scoped>
.tab-bar-item {
  flex: 1;
  text-align: center;
  height: 49px;
  font-size: 14px;
}

.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  margin-bottom: 2px;
  /* 清除图片下BUG的3px */
  vertical-align: middle;
}

/* .active {
  color: deeppink;
} */
</style>
