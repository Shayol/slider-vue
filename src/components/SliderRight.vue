<template>

  <div class="slider slider--right">
   <div class="slider__content">
      <div ref="img_0" class="slider__img slider__img--small slider__img-1"></div>
      <div ref="img_1" class="slider__img slider__img--medium slider__img-2"></div>
      <div ref="img_2" class="slider__img slider__img--big slider__img-3"></div>
      <div ref="img_3" class="slider__img slider__img--medium slider__img-4"></div>
      <div ref="img_4" class="slider__img slider__img--small slider__img-5"></div>
    </div>
    <button class="slider__shuffle">
        Shuffle
    </button>
  </div>
</template>

<script>
export default {
  name: "SliderRight",
  props: ["imgs"],
  mounted() {
    let self = this;
    let k = 1;

    setTimeout(animation, 2500);

    async function animation() {
      let n = k;

      for (let i = 0, l = 5; i < l; i++) {
        self.$refs[`img_${i}`].style.opacity = "0";
      }

      await new Promise(resolve => {
        setTimeout(() => {
          for (let i = 0, l = 5; i < l; i++, n++) {
            if (n >= self.indexesR.length) {
              n = 0;
            }

            self.$refs[`img_${i}`].style.backgroundImage = `url(${
              self.imgs[self.indexesR[n]]
            })`;
            self.$refs[`img_${i}`].style.opacity = "1";
          }

          resolve();
        }, 700);
      });

      k++;
      if (k >= self.indexesR.length) {
        k = 0;
      }
      setTimeout(animation, 2500);
    }
  },
  data: function() {
    return {
      indexesR: [...this.imgs.keys()]
    };
  },
  watch: {
    imgs: function(val) {
      this.indexesR.push(val.length - 1);
    }
  },
  computed: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.slider {
  margin-bottom: 5%;
  &__content {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    height: 200px;
  }
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
    &-1 {
      background-image: url("../assets/image-1.jpg");
    }
    &-2 {
      background-image: url("../assets/image-2.jpg");
    }
    &-3 {
      background-image: url("../assets/image-3.jpg");
    }
    &-4 {
      background-image: url("../assets/image-4.jpg");
    }
    &-5 {
      background-image: url("../assets/image-5.jpg");
    }
    &\--big {
      width: 30%;
      height: 100%;
    }
    &\--medium {
      width: 15%;
      height: 50%;
    }
    &\--small {
      width: 5%;
      height: 25%;
    }
  }
  &__shuffle {
    width: 30%;
    margin-left: auto;
    margin-right: auto;
    display: block;
    margin-top: 20px;
  }
}
</style>
