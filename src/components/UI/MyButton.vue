<template>
  <button class="btn" :class="{ pressed: state }">{{ message }}</button>
</template>

<script>
export default {
  name: "my-button",
  data() {
    return {
      message: "Выбрать",
    };
  },
  props: {
    state: {
      type: Boolean,
    },
  },
  watch: {
    state() {
      if (this.state) {
        this.message = "Выбрано";
      } else {
        this.message = "Выбрать";
      }
    },
  },
};
</script>
<style scoped>
.btn {
  border: none;
  width: 100%;
  height: 2rem;
  border-radius: 0.25rem;
  color: #fff;
  transition: all 0.3s linear;
  background: rgb(137, 146, 171);
}

.pressed {
  background: #2fcb5a;
}
</style>
