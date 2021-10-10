<template>
  <div class="ui secondary menu">
    <div class="ui container">
      <div class="left menu">
        <router-link class="item" to="/">
          <img class="ui small image" src="../assets/logo.png" alt="Ecomerce" />
        </router-link>
        <template v-for="category in categories" :key="category.id">
          <router-link class="item" :to="category.slug">
            {{ category.title }}
          </router-link>
        </template>
      </div>
      <!-- Iniciar sesion -->
      <div class="right menu">
        <router-link class="item" to="/login" v-if="!token">
          Iniciar sesión
        </router-link>

        <template v-if="token">

          <span class="ui item cart">
            <i class="shopping cart icon" @click="openCart"></i>
          </span>
          <span class="ui item logout" @click="logout">
            <i class="sign-out icon"></i>
          </span>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { useStore } from 'vuex';
import { getTokenApi, deleteTokenApi } from '../api/token';
import { getCategoriesApi } from '../api/category';

export default {
  name: 'Menu',

  setup() {
    let categories = ref(null);
    const token = getTokenApi();
    const store = useStore();

    onMounted(async () => {
      const response = await getCategoriesApi();
      categories.value = response;
    });

    const logout = () => {
      deleteTokenApi();
      location.replace('/');
    };

    const openCart = () => {
      store.commit('setShowCart', true);
    };

    return {
      token,
      logout,
      categories,
      openCart,
    };
  },
};
</script>

<style lang="scss" scoped>
* {
  color: #ffffff;
}
.ui.menu.secondary {
  background-image: url('https://drncvpyikhjv3.cloudfront.net/sites/131/2016/09/21101909/blue-background-header-1.png');

  .item {
    color: #ffffff;
    &:hover {
      color: #1fa1f1;
    }
  }

  .menu.left {
    width: 50%;
    .ui.image {
      width: 120px;
    }
  }

  .menu.right {
    width: 50%;
    justify-content: flex-end;

    .logout,
    .cart {
      &:hover {
        cursor: pointer;
      }
    }
  }
}
</style>
