<template>
  <div class="card">
    <img class="img" :src="product.images[0].src" alt="" />
    <div class="name">{{ filterText(product.name) }}</div>
    <div class="categories">{{ getCategories(product.categories) }}</div>
    <div class="desc">{{ filterText(product.short_description) }}</div>
    <div class="button">
      <div class="price">{{ product.prices.price + "  " + product.prices.currency_symbol }}</div>
      <AddToCart :url="cartUrl"></AddToCart>
    </div>
  </div>
</template>
<script>
import AddToCart from "./AddToCartComponent.vue";

export default {
  name: "CardComponent",
  data () {
    return {
      cartUrl: 'https://greet.bg/?add-to-cart=5589'
    };
  },
  components: {
    AddToCart,
  },
  props: {
    product: Object,
  },
  methods: {
    getCategories(categories) {
      return categories.map((category) => category.name).join(", ");
    },
    filterText(text) {
      return text.replace(
        /<\/?p>|&#8220|&#8221|&#8211|;|<br>|<\/br>|<br\s*\/?>/g,
        ""
      );
    },
  },
};
</script>
<style lang="scss">
@import "../styles/CardComponent.scss";
</style>
