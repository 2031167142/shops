<template>
  <header>
    <h2 ref="hh" @click="hs1">{{ title }}</h2>
  </header>
</template>

<script>
export default {
  props: {
    title: {
      default: "",
      type: String,
    },
  },
  methods: {
    hs1() {
      if (this.$refs.hh.style.color == "green") {
        this.$refs.hh.style.color = "white";
      } else {
        this.$refs.hh.style.color = "green";
      }
    },
  },
};
</script>

<style scoped>
h2 {
  text-align: center;
  width: 100%;
  height: 100%;
  background-color: rgb(0, 140, 255);
  color: white;
  line-height: 12vh;
}
</style>