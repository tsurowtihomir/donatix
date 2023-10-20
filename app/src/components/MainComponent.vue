<template>
  <div class="content">
    <div class="cardComponent"  v-for="product in products" :key="product.name">
      <CardComponent :product="product"></CardComponent>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardComponent from './CardComponent.vue'

export default {
  components: {
    CardComponent,
  },
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get("https://greet.bg/wp-json/wc/store/products?page=1")
        .then((response) => {
          this.products = response.data;
          console.log(this.products)
        })
        .catch((error) => {
          console.error("Error fetching data", error);
        });
    },
  },
};
</script>

<style>
.content{
  display: flex;
  flex-wrap: wrap;
  padding: 10px;
  text-align: center;
}
.cardComponent{
  flex: 1 0 18%;
  display: flex;
  justify-content: center;
}
</style>
