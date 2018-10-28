<template>
  <div id="app" class="container">
    <Slider :imgs="imgs" direction="left"/>
    <Slider :imgs="imgs" direction="right"/>    
  </div>
</template>

<script>
import Slider from "./components/Slider.vue";

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
    Slider
  }
};
</script>

<style lang="scss">
</style>
