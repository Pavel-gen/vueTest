<template>
  <div :class="{ notBright: this.currentIndex >= this.index }">
    <div :class="{ hidden_varint: this.currentIndex >= this.index }"></div>
    <div class="main_title">{{ example.title }}</div>
    <my-variant
      ref="listEl"
      v-for="variant in example.variants"
      :variant="variant"
      :key="variant.title"
      @pressedButton="changedPrice"
    />
  </div>
</template>

<script>
import MyVariant from "./MyVariant.vue";
export default {
  components: {
    MyVariant,
  },
  name: "my-list",
  props: {
    example: {
      type: Object,
    },
    modelValue: {
      type: [Number, String],
    },
    arr: {
      type: Array,
    },
    index: {
      type: [Number, String],
    },
  },

  methods: {
    changedPrice(event) {
      this.$emit("updateIndex", this.currentIndex + 1);

      console.log(event);
      let result;
      if (event[1]) {
        result = this.modelValue + event[0];
        this.$emit("update:modelValue", this.modelValue + event[0]);
      } else {
        result = this.modelValue - event[0];
        console.log(this.modelValue);
        console.log(event[0]);
        this.$emit("update:modelValue", this.modelValue - event[0]);
      }

      if (event[1]) {
        console.log("lskldfk");
        setTimeout(() => {
          this.doForFun(event[2], event[3]);
        }, 10);
      }
    },

    doForFun(title) {
      let elements = this.$refs.listEl;
      elements = elements.filter((item) => item.variant.title !== title);
      elements.forEach((el) => {
        if (el.pressed) {
          el.clickButton();
        }
        console.log(elements);
      });
    },
  },

  computed: {
    currentIndex() {
      return this.arr.indexOf(this.example);
    },
  },
};
</script>
<style scoped>
.hidden_varint {
  background: rgba(0, 0, 0, 0.03);
  z-index: 5;
  height: 63%;
  position: absolute;
  border-radius: 0.25rem;
  width: calc(100% - 4rem);
  max-width: 50rem;
  margin-top: -1rem;
  transition: all 0.3s linear;
}

.notBright {
  color: rgb(139, 128, 128);
}
</style>
