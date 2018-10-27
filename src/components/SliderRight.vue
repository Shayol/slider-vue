<template>

  <div class="slider slider--right">
   <div class="slider__content">
      <div :style="img_0" ref="img_0" class="slider__img slider__img--small slider__img-1"></div>
      <div :style="img_1" ref="img_1" class="slider__img slider__img--medium slider__img-2"></div>
      <div :style="img_2" ref="img_2" class="slider__img slider__img--big slider__img-3"></div>
      <div :style="img_3" ref="img_3" class="slider__img slider__img--medium slider__img-4"></div>
      <div :style="img_4" ref="img_4" class="slider__img slider__img--small slider__img-5"></div>
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

            self[`n_${i}`] = n;
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
      indexesR: [...this.imgs.keys()],
      n_0: 0,
      n_1: 1,
      n_2: 2,
      n_3: 3,
      n_4: 4
    };
  },
  watch: {
    imgs: function(val) {
      this.indexesR.push(val.length - 1);
    }
  },
  computed: {
    img_0() {
      let backgroundImage = `url(${this.imgs[this.indexesR[this.n_0]]})`;
      return { backgroundImage };
    },
    img_1() {
      let backgroundImage = `url(${this.imgs[this.indexesR[this.n_1]]})`;
      return { backgroundImage };
    },
    img_2() {
      let backgroundImage = `url(${this.imgs[this.indexesR[this.n_2]]})`;
      return { backgroundImage };
    },
    img_3() {
      let backgroundImage = `url(${this.imgs[this.indexesR[this.n_3]]})`;
      return { backgroundImage };
    },
    img_4() {
      let backgroundImage = `url(${this.imgs[this.indexesR[this.n_4]]})`;
      return { backgroundImage };
    }
  }
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
    // &-1 {
    //   background-image: url("./image-1.jpg");
    // }
    // &-2 {
    //   background-image: url("./image-2.jpg");
    // }
    // &-3 {
    //   background-image: url("./image-3.jpg");
    // }
    // &-4 {
    //   background-image: url("./image-4.jpg");
    // }
    // &-5 {
    //   background-image: url("./image-5.jpg");
    // }
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
