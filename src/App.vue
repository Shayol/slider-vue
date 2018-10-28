<template>
  <div id="app" class="container">
    <form class="upload" method="post" enctype="multipart/form-data">
        <div>
            <label class="upload__label" for="img-upload">Choose img to upload</label>
            <input ref="upload" @change="uploadImg" type="file" id="img-upload" class="upload__field" name="img" accept=".jpg, .jpeg, .png">
        </div>
    </form>
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
  },
  methods: {
    uploadImg(e) {
      let src = window.URL.createObjectURL(e.target.files[0]);
      this.imgs.push(src);
    }
  }
};
</script>

<style lang="scss">
.upload {
  position: relative;
  display: block;
  margin-bottom: 20%;

  &__label {
    background-color: antiquewhite;
    border: 1px solid black;
    display: block;
    height: 32px;
    width: 100%;
    line-height: 32px;
    text-align: center;
    padding-left: 4px;
    padding-right: 4px;
  }
  &__field {
    visibility: hidden;
    z-index: -1;
    position: absolute;
  }
  @media (min-width: $tablet) {
    margin-bottom: 2%;
    &__label {
      width: auto;
      display: inline-block;
    }
  }
}
</style>
