<template>
  <select @change="selectFunc" class="mySelect">
    <option :value="item.price" v-for="item in items" :key="item.title">
      {{ item.title }}
    </option>
  </select>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      default: () => [],
    },
    modelValue: {
      type: [String, Number],
    },
  },
  methods: {
    selectFunc(event) {
      this.$emit("update:modelValue", parseInt(event.target.value));
    },
  },
};
</script>
<style scoped>
.mySelect {
  width: 100%;
  padding: 0.35rem 0.45rem;
  border-radius: 0.25rem;
  margin-bottom: 0.5rem;
}
</style>
