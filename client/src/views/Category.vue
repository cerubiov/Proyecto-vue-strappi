<template>
  <BasicLayouts>
    <div class="ui grid">
      <div
        class="sixten wide mobile eight wide tablet four wide computer column"
        v-for="product in products"
        :key="product.id"
      >
        <Product :product="product" />
      </div>
    </div>
  </BasicLayouts>
</template>

<script>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import BasicLayouts from '../layouts/BasicLayouts.vue';
import Product from '../components/Product.vue';
import { getCategoriesApi, getProductsCategory } from '../api/product';

export default {
  name: 'Category',
  components: {
    BasicLayouts,
    Product,
  },

  watch: {
    $route(to, from) {
      this.getProduts(to.params.category);
    },
  },

  setup() {
    let products = ref(null);
    const { params } = useRoute();

    onMounted(() => {
      getProduts(params.category);
    });

    const getProduts = async (categoty) => {
      const response = await getProductsCategory(categoty);
      products.value = response;
    };

    return {
      getProduts,
      products,
    };
  },
};
</script>
