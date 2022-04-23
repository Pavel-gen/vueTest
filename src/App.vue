<template>
  <div class="app">
    <div class="container" v-for="example in examples" :key="example.title">
      <my-list
        v-model="final_price"
        :index="postIndex"
        :example="example"
        :arr="examples"
        @updateIndex="changeIndex"
      ></my-list>
    </div>
    <div class="total_price">
      <div>Итого к оплате</div>
      <div class="price">{{ final_price }}</div>
    </div>
  </div>
</template>

<script>
import MyList from "./components/MyList.vue";
const data = require("../data.json");

console.log(data);
export default {
  components: { MyList },
  data() {
    return {
      examples: data,
      final_price: 0,
      postIndex: 1,
    };
  },

  methods: {
    changeIndex(event) {
      this.postIndex = event + 1;
      console.log(this.postIndex);
    },
  },
};
</script>
1
<style>
*,
::before,
::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.price::after {
  content: " \20BD";
}

.container {
  border-top: 3px solid rgb(189, 186, 186);
  margin-left: 2rem;
  margin-right: 2rem;
  margin-top: 2rem;
  padding-top: 0.75rem;
}

.app {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-bottom: 10rem;
  font-family: Arial, Helvetica, sans-serif;
}

.total_price {
  width: 90%;
  margin: 1rem;
  background: #2fcb5a;
  position: fixed;
  bottom: 0;
  display: flex;
  padding: 1rem 2rem;
  justify-content: space-between;
  color: #fff;
  font-size: 1.75rem;
  text-transform: uppercase;
  max-width: 60rem;
  border-radius: 0.25rem;
  font-weight: 700;
  z-index: 20;
}

.main_title {
  font-weight: 700;
}
</style>
