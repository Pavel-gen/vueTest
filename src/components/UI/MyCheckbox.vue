<template>
  <div class="inputContainer">
    <input
      class="specInput"
      ref="neededCheckbox"
      type="checkbox"
      @change="doCheckbox"
    />
    <label class="specLabel">{{ option.title }}</label>
  </div>
</template>

<script>
export default {
  name: "my-checkbox",

  props: {
    option: {
      type: Object,
    },
    pressed: {
      type: Boolean,
    },

    modelValue: {
      type: [String, Number],
    },
  },
  methods: {
    doCheckbox(event) {
      this.checked = !this.checked;
      this.$emit("takeCheckbox", [this.option.price, this.checked]);
      this.$emit("update:modelValue", [this.option.price, this.checked]);
    },
  },
  data() {
    return {
      checked: false,
    };
  },
};
</script>
<style scoped>
.inputContainer {
  border: 1px solid #000;
  width: 100%;
  padding: 0.35rem 0.45rem;
  border-radius: 0.25rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.specLabel {
  width: 100%;
  text-align: center;
}
</style>
