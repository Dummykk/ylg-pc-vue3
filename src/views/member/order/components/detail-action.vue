<template>
  <div class="detail-action">
    <div class="state">
      <span
        class="iconfont"
        :class="[`icon-order-${orderStatus[order.orderState].name}`]"
      >
      </span>
      <p>{{ orderStatus[order.orderState].label }}</p>
    </div>
    <div class="info">
      <p>订单编号：{{ order.id }}</p>
      <p>下单时间：{{ order.createTime }}</p>
    </div>
    <div class="btn">
      <template v-if="order.orderState === 1">
        <xtx-button
          @click="$router.push('/member/pay?id=' + order.id)"
          type="primary"
          size="small"
        >
          立即付款
        </xtx-button>
        <xtx-button type="gray" size="small" @click="handlerCancel(order)">
          取消订单
        </xtx-button>
      </template>
      <!-- 待发货 -->
      <template v-if="order.orderState === 2">
        <xtx-button
          type="primary"
          size="small"
          @click="$router.push(`/member/checkout?orderId=${order.id}`)"
          >再次购买</xtx-button
        >
      </template>
      <!-- 待收货 -->
      <template v-if="order.orderState === 3">
        <xtx-button type="primary" size="small">确认收货</xtx-button>
        <xtx-button
          type="plain"
          size="small"
          @click="$router.push(`/member/checkout?orderId=${order.id}`)"
          >再次购买</xtx-button
        >
      </template>
      <!-- 待评价 -->
      <template v-if="order.orderState === 4">
        <xtx-button
          type="primary"
          size="small"
          @click="$router.push(`/member/checkout?orderId=${order.id}`)"
          >再次购买</xtx-button
        >
        <xtx-button type="plain" size="small">评价商品</xtx-button>
        <xtx-button type="gray" size="small">申请售后</xtx-button>
      </template>
      <!-- 已完成 -->
      <template v-if="order.orderState === 5">
        <xtx-button
          type="primary"
          size="small"
          @click="$router.push(`/member/checkout?orderId=${order.id}`)"
          >再次购买</xtx-button
        >
        <xtx-button type="plain" size="small">查看评价</xtx-button>
        <xtx-button type="gray" size="small">申请售后</xtx-button>
      </template>
    </div>
    <!-- 取消订单 -->
    <order-cancel ref="orderCancelCom" />
  </div>
</template>

<script>
import { orderStatus } from '@/api/constants'
import { useCancel, useConfirmReceipt } from '../index.vue'
import orderCancel from './order-cancel.vue'

export default {
  components: { orderCancel },
  name: 'OrderDetailAction',

  props: {
    order: {
      type: Object,
      default: () => {}
    }
  },

  setup () {
    return { orderStatus, ...useCancel(), ...useConfirmReceipt() }
  }
}
</script>

<style lang='less' scoped>
.detail-action {
  height: 180px;
  width: 100%;
  display: flex;
  align-items: center;
  .state {
    width: 220px;
    text-align: center;
    .iconfont {
      font-size: 40px;
      color: @xtxColor;
    }
    p {
      font-size: 16px;
      color: #666;
      margin-bottom: 10px;
    }
  }
  .info {
    width: 240px;
    line-height: 30px;
    p {
      color: #999;
    }
  }
  .btn {
    flex: 1;
    text-align: right;
    margin-right: 100px;
    .xtx-button {
      margin-left: 20px;
    }
  }
}
</style>
