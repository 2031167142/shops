<template>
  <div class="nav-bottom">
    <div>
      <input
        type="checkbox"
        id="ff"
        style="margin-right: 2px"
        :checked="isfull"
        @change="fullChange"
      />
      <label for="ff">全选</label>
    </div>
    <!-- 商品总价格 -->
    <div style="margin-left: -3px">
      合计：
      <h5>￥{{ totalPrice.toFixed(2) }}</h5>
    </div>
    <!-- 商品总数量 -->
    <div>
      <button>结算（{{ totalCount }}）</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isfull: {
      type: Boolean,
      default: true,
    },
    totalPrice: {
      type: Number,
      default: 0,
    },
    totalCount: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    fullChange(e) {
      this.$emit("full-change", e.target.checked);
    },
  },
};
</script>

<style lang="less" scope>
.nav-bottom {
  background-color: rgb(236, 236, 236);
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 14px;
  div {
    flex: 1.5;
    display: flex;
    justify-content: center;
    align-items: center;
    h5 {
      color: red;
    }
    button {
      width: 90%;
      height: 100%;
      border: 1px rgb(0, 110, 255) solid;
      border-radius: 360px;
      background-color: rgb(0, 110, 255);
      color: white;
      vertical-align: middle;
      padding: 5px;
    }
  }
  div:first-child {
    flex: 1;
  }
}
</style>