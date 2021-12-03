<template>
  <div id="app">
    <!-- 头部 -->
    <div class="header-box">
      <Header title="购物车案例"></Header>
    </div>

    <!-- body -->
    <div class="gooods-box">
      <Goods
        v-for="item in list"
        :key="item.id"
        :id="item.id"
        :title="item.goods_name"
        :pic="item.goods_img"
        :price="item.goods_price"
        :state="item.goods_state"
        @state-change="getNewState"
      >
        <Counter
          :num="item.goods_count"
          :id="item.id"
          @num-change="getNewNum"
        ></Counter>
      </Goods>
    </div>

    <!-- 页脚 -->
    <!-- 这个div用来站位的  因为页脚是固定定位 没有实际面积 -->
    <div style="width: 100vw; height: 9vh"></div>
    <div class="footer-box">
      <Footer
        :isfull="fullState"
        :totalPrice="totalPrice"
        :totalCount="totalCount"
        @full-change="getFullState"
      ></Footer>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "@/components/ShoppingCart/Header";
import Goods from "@/components/ShoppingCart/Goods";
import Footer from "@/components/ShoppingCart/Footer";
import Counter from "@/components/ShoppingCart/Counter";

export default {
  data() {
    return {
      list: [],
    };
  },
  name: "App",
  // 注册组件
  components: {
    Header,
    Goods,
    Footer,
    Counter,
  },
  // 计算属性
  computed: {
    // 计算商品是否全选了
    fullState() {
      return this.list.every((item) => item.goods_state);
    },
    //计算选中的商品的价格总和
    totalPrice() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce(
          (total, item) => (total += item.goods_price * item.goods_count),
          0
        );
    },
    // 计算勾选的商品的数量
    totalCount() {
      return this.list
        .filter((item) => item.goods_state)
        .reduce((total, item) => (total += item.goods_count), 0);
    },
  },
  created() {
    this.initCartList();
  },
  methods: {
    async initCartList() {
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");

      if (res.status === 200) {
        this.list = res.list;
      }
    },
    // 接受子组件传过来的参数
    getNewState(e) {
      // console.log(e);
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_state = e.value;

          // 终止后面循环
          return true;
        }
      });
    },
    // 接受全选按钮状态
    getFullState(e) {
      this.list.forEach((item) => {
        item.goods_state = e;
      });
    },
    // 获取到Counter组件传来的值
    getNewNum(e) {
      this.list.some((item) => {
        if (item.id === e.id) {
          item.goods_count = e.num;

          // 终止后面循环
          return true;
        }
      });
    },
  },
};
</script>

<style lang="less">
* {
  margin: 0;
  padding: 0;
}
.header-box {
  width: 100vw;
  height: 12vh;
}
.gooods-box {
  width: 100vw;
}
.footer-box {
  width: 100vw;
  height: 9vh;
  // 固定定位
  position: fixed;
  bottom: 0;
  left: 0;
}
</style>
