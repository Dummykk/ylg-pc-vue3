<template>
  <div class="xtx-tabs-panel" v-show="activeName === name">
    <slot />
  </div>
</template>

<script>
import { inject } from 'vue'
export default {
  name: 'XtxTabsPanel',

  props: {
    // 标签页标题
    label: {
      type: String,
      default: ''
    },
    // 唯一标识
    name: {
      type: String,
      default: ''
    }
  },

  setup () {
    const activeName = inject('activeName')
    return { activeName }
  }
}
</script>

<style lang='less' scoped>
</style>
