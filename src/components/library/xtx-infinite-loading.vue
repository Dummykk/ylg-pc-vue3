<template>
  <div class="xtx-infinite-loading" ref="box">
    <div class="loading" v-if="loading">
      <span class="img"></span>
      <span class="text">正在加载...</span>
    </div>
    <div class="none" v-if="finished">
      <span class="img"></span>
      <span class="text">亲，没有更多了</span>
    </div>
  </div>
</template>

<script>
import { useIntersectionObserver } from '@vueuse/core'
import { ref } from 'vue'

export default {
  name: 'XtxInfiniteLoading',

  props: {
    loading: {
      type: Boolean,
      default: false
    },
    finished: {
      type: Boolean,
      default: false
    }
  },

  setup (props, { emit }) {
    const box = ref(null)

    useIntersectionObserver(
      box,
      ([{ isIntersecting }]) => {
        if (isIntersecting) {
          if (!props.loading && !props.finished) {
            emit('infinite')
          }
        }
      },
      { threshold: 0 }
    )

    return { box }
  }
}
</script>

<style lang='less' scoped>
.xtx-infinite-loading {
  .loading {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 200px;
    .img {
      width: 100px;
      height: 178px;
      background: url(~@/assets/images/loading.gif) no-repeat center / 100px
        178px;
    }
    .text {
      color: #999;
      font-size: 16px;
    }
  }
  .none {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 200px;
    .img {
      width: 200px;
      height: 134px;
      background: url(~@/assets/images/none.png) no-repeat center / contain;
    }
    .text {
      color: #999;
      font-size: 16px;
    }
  }
}
</style>
