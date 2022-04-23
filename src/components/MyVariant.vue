<template>
  <div ref="variant" class="variant">
    <div class="variant_title">
      <h3>{{ variant.title }}</h3>
      <div class="price">{{ localPrice }}</div>
    </div>
    <div class="inner_variant" :class="{ choosen_style: pressed }">
      <div class="description">
        <p v-for="sentence in slpitDescription" :key="sentence">
          {{ sentence }}
        </p>
      </div>
      <div class="right_part">
        <form>
          <fieldset ref="formPart" class="fieldset">
            <my-checkbox
              v-for="option in variant.options"
              v-model="optionPrice"
              :key="option.title"
              :option="option"
              @takeCheckbox="doSomething"
              :choosed="choosed"
              :title="variant.title"
            >
            </my-checkbox>
            <div
              v-for="selectOption in variant.select"
              :key="selectOption.title"
            >
              <my-select v-model="selectPrice" :items="selectOption.items">
              </my-select>
            </div>
          </fieldset>
        </form>
        <my-button :state="pressed" @click="clickButton"></my-button>
      </div>
    </div>
  </div>
</template>

<script>
import MyButton from "./UI/MyButton.vue";
import MyCheckbox from "./UI/MyCheckbox.vue";
import MySelect from "./UI/MySelect.vue";

export default {
  components: { MyCheckbox, MyButton, MySelect },
  data() {
    return {
      selectPrice: 0,
      optionPrice: 0,
      totalOption: 0,

      pressed: false,
    };
  },
  props: {
    variant: {
      type: Object,
    },
  },
  methods: {
    clickButton() {
      this.pressed = !this.pressed;
      this.$emit("pressedButton", [
        this.localPrice,
        this.pressed,
        this.variant.title,
      ]);
    },
  },
  computed: {
    slpitDescription() {
      return this.variant.description.split("\n");
    },
    localPrice() {
      return this.variant.price_default + this.selectPrice + this.totalOption;
    },
  },
  watch: {
    selectPrice(event) {
      console.log(event);
    },
    optionPrice(event) {
      event[1]
        ? (this.totalOption += event[0])
        : (this.totalOption -= event[0]);
    },
    pressed(value) {
      let el = this.$refs.formPart;
      if (value) {
        el.disabled = true;
      } else {
        el.disabled = false;
      }
    },
  },
  mounted() {
    this.$refs.variant.style.setProperty("--left-color", this.variant.color);
  },
};
</script>

<style scoped>
.variant {
  z-index: -9;
  width: 100%;
  max-width: 50rem;
  background: rgb(247, 243, 243);
  padding: 0.85rem;
  margin-top: 0.75rem;
  border-radius: 0.25rem;
  border-left: 0.5rem solid var(--left-color);
}

.fieldset {
  border: none;
  background: none;
}
.inner_variant {
  display: flex;
  justify-content: space-between;
  margin-top: 0.5rem;
  transition: all 0.3s linear;
}
.right_part {
  padding-left: 1rem;
  min-width: 30%;
  display: flex;
  flex-direction: column;
  border-left: 1px solid #000;
}

@media screen and (max-width: 700px) {
  .right_part {
    min-width: 12rem;
  }
}

.description {
  padding-right: 0.5rem;
}
.description p {
  margin-bottom: 0.75rem;
}

.variant_title {
  display: flex;
  justify-content: space-between;
}

.choosen_style {
  color: rgb(108, 107, 107);
}
</style>
