<template>

  <div class="slider slider--right">
   <div class="slider__content">
      <ImgComp v-for="(item,index) in styles" :key="index" :img-style="item" :img-class="classes[index]"/>
    </div>
    <button @click="shuffle" class="slider__shuffle">
        Shuffle
    </button>
  </div>
</template>

<script>
import ImgComp from "./ImgComp.vue";
import shuffleArray from "../shufflearray.js";
export default {
  name: "Slider",
  props: ["imgs", "direction"],
  components: {
    ImgComp
  },
  data: function() {
    return {
      indexes: [...this.imgs.keys()],
      timerID: "",
      styles: [
        {
          backgroundImage: "url('./image-1.jpg')",
          opacity: 1
        },
        {
          backgroundImage: "url('./image-2.jpg')",
          opacity: 1
        },
        {
          backgroundImage: "url('./image-3.jpg')",
          opacity: 1
        },
        {
          backgroundImage: "url('./image-4.jpg')",
          opacity: 1
        },
        {
          backgroundImage: "url('./image-5.jpg')",
          opacity: 1
        }
      ],
      classes: [
        "slider__img--small",
        "slider__img--medium",
        "slider__img--big",
        "slider__img--medium",
        "slider__img--small"
      ]
    };
  },
  mounted() {
    this.init();
  },
  watch: {
    imgs: function(val) {
      this.indexes.push(val.length - 1);
    }
  },
  computed: {},
  methods: {
    shuffle() {
      clearTimeout(this.timerID);
      shuffleArray(this.indexes);
      for (let i = 0, l = 5; i < l; i++) {
        this.styles[i].backgroundImage = `url(${this.imgs[this.indexes[i]]})`;
        this.styles[i].opacity = "1";
      }
      this.init();
    },
    init() {
      let self = this;
      let k;

      if (self.direction == "right") {
        k = 1;
      } else {
        k = self.indexes.length - 1;
      }

      self.timerID = setTimeout(animation, 2500);

      async function animation() {
        let n = k;

        for (let i = 0, l = 5; i < l; i++) {
          self.styles[i].opacity = "0";
        }

        await new Promise(resolve => {
          setTimeout(() => {
            for (let i = 0, l = 5; i < l; i++, n++) {
              if (n >= self.indexes.length) {
                n = 0;
              }

              self.styles[i].backgroundImage = `url(${
                self.imgs[self.indexes[n]]
              })`;
              self.styles[i].opacity = "1";
            }

            resolve();
          }, 700);
        });

        if (self.direction == "right") {
          k++;
          if (k >= self.indexes.length) {
            k = 0;
          }
        } else {
          k--;
          if (k < 0) {
            k = self.indexes.length - 1;
          }
        }

        self.timerID = setTimeout(animation, 2500);
      }
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
  &__shuffle {
    width: 30%;
    margin-left: auto;
    margin-right: auto;
    display: block;
    margin-top: 20px;
  }
}
</style>
