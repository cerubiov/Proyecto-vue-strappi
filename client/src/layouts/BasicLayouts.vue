<template>
  <div class="basic-layaout">
    <Menu />
    <div class="ui container">
      <slot />
    </div>
  </div>

  <Cart />
</template>

<script>
import Menu from '../components/Menu.vue';
import Cart from '../components/Cart/Cart.vue';
export default {
  name: 'BasicLayouts',

  components: {
    Menu,
    Cart,
  },
};
</script>

<style></style>
