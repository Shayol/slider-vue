<template>
  <div id="app">
    <slider-right :imgs="imgs"/>
    <slider-left :imgs="imgs"/>
  </div>
</template>

<script>
import SliderRight from "./components/SliderRight.vue";
import SliderLeft from "./components/SliderLeft.vue";

export default {
  name: "app",
  data: function() {
    return {
      imgs: [
        "./image-1.jpg",
        "./image-2.jpg",
        "./image-3.jpg",
        "./image-4.jpg",
        "./image-5.jpg"
      ]
    };
  },
  components: {
    SliderRight,
    SliderLeft
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
