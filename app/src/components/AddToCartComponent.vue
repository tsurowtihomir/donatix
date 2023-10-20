<template>
  <a :href="url">
    <button class="add">
      <img class="cartImg" src="../assets/cart.png" alt="" />
      Add To Cart
    </button>
  </a>
</template>
<script>
export default {
  name: "AddToCardComponent",
  props: {
    url: String,
  },
};
</script>
<style lang="scss">
@import "../styles/AddToCardComponent.scss";
</style>
