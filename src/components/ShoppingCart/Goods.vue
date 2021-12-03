<template>
  <div class="box">
    <!-- 单选框 -->
    <div>
      <input
        type="checkbox"
        :id="'sb' + id"
        :checked="state"
        @change="getNewState"
      />
      <label :for="'sb' + id"></label>
    </div>

    <!-- 商品图片 -->
    <div>
      <img :src="pic" alt="图片" />
    </div>

    <div class="ts">
      <!-- 商品标题 -->
      <p>{{ title }}</p>

      <div>
        <!-- 商品单价 -->
        <h5>￥{{ price }}</h5>
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      required: true,
      type: Number,
    },
    title: {
      deflute: "",
      type: String,
    },
    pic: {
      deflute: "",
      type: String,
    },
    price: {
      deflute: 0,
      type: Number,
    },
    state: {
      deflute: true,
      type: Boolean,
    },
  },
  methods: {
    // 只要复选框发送变化 就会调用这个函数
    getNewState(e) {
      const newState = e.target.checked;
      // 触发自定义事件
      this.$emit("state-change", { id: this.id, value: newState });
    },
  },
};
</script>

<style lang="less" scoped>
.box {
  display: flex;
  // margin-top: 10px;
  // margin-bottom: 10px;

  div {
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 5px;
  }
  .ts {
    align-items: flex-start;
    justify-content: space-between;
    flex-flow: column;
    font-size: 13px;
    font-weight: bold;
    display: flex;
    div {
      display: flex;
      width: 100%;
    }
  }
}

img {
  width: 30vw;
}
h5 {
  color: red;
}
</style>