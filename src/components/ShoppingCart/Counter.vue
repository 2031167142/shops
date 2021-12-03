<template>
  <div class="box" style="margin-left: 80px">
    <!-- 减1的按钮 -->
    <input type="button" value="-" @click="sub" />
    <!-- 商品购买数量 -->
    <span>{{ num }}</span>
    <!-- 加1的按钮 -->
    <input type="button" value="+" @click="add" />
  </div>
</template>

<script>
export default {
  props: {
    num: {
      type: Number,
      default: 1,
    },
    id: {
      type: Number,
      default: null,
    },
  },
  methods: {
    add() {
      this.$emit("num-change", { num: this.num + 1, id: this.id });
    },
    sub() {
      if (this.num === 0) {
        return true;
      }
      this.$emit("num-change", { num: this.num - 1, id: this.id });
    },
  },
};
</script>

<style lang="less" scoped>
.box {
  text-align: center;
  input {
    width: 20px;
  }
  span {
    width: 30px;
  }
}
</style>

