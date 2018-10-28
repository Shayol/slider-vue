<template>
    <div :class="imgClass" :style="imgStyle" class="slider__img">

    </div>
</template>
<script>
export default {
  name: "ImgComp",
  props: ["imgStyle", "imgClass"]
};
</script>
<style lang="scss">
.slider {
  &__img {
    border: 1px solid black;
    background-position: center;
    background-size: cover;
    font-size: 30px;
    text-align: center;
    color: white;
    font-weight: bold;
    opacity: 1;
    transition: opacity 0.7s ease-in;
    &\--big {
      width: 45%;
      height: 100%;
    }
    &\--medium {
      width: 15%;
      height: 50%;
    }
    &\--small {
      width: 10%;
      height: 25%;
    }
  }
}
</style>

