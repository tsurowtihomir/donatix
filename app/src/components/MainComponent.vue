<template>
  <div class="filters">
    <div class="categories">
      <select v-model="selectedCategory" @change="filterCards">
        <option value="">All Categories</option>
        <option v-for="(category, index) in allCategories" :value="category" :key="index">
          {{ category }}
        </option>
      </select>
    </div>
    <div class="orderBy">
      <select v-model="selectedOrder" @change="orderBy">
        <option value="">Order By</option>
        <option value="name">Name</option>
        <option value="price">Price</option>
      </select>
    </div>
  </div>
  <div class="content">
    <div class="cardComponent" v-for="product in sortedProducts" :key="product.name">
      <CardComponent :product="product"></CardComponent>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CardComponent from "./CardComponent.vue";

export default {
  components: {
    CardComponent,
  },
  data() {
    return {
      products: [],
      selectedCategory: "",
      selectedOrder: "",
    };
  },
  computed: {
    filteredProducts() {
      if (!this.selectedCategory) {
        return this.products;
      }
      return this.products.filter((product) =>
        product.categories.some((category) => category.name === this.selectedCategory)
      );
    },
    allCategories() {
      const categories = new Set();
      this.products.forEach((product) => {
        product.categories.forEach((category) => {
          categories.add(category.name);
        });
      });
      return Array.from(categories);
    },
    sortedProducts() {
      if (this.selectedOrder === 'name') {
        return [...this.filteredProducts].sort((a, b) => a.name.localeCompare(b.name));
      } else if (this.selectedOrder === 'price') {
        return [...this.filteredProducts].sort((a, b) => a.prices.price - b.prices.price);
      }
      return this.filteredProducts;
    },
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
        })
        .catch((error) => {
          console.error("Error fetching data", error);
        });
    },
  },
};
</script>

<style lang="scss">
@import "../styles/MainComponent.scss";
</style>
