<script setup lang="ts">
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { RouterLink, useRouter } from 'vue-router'

const router = useRouter();
const isLoggedIn = localStorage.getItem('isLoggedIn') == 'true';

const logoutButton = () => {
  localStorage.removeItem('account_id');
  localStorage.setItem('isLoggedIn', 'false');
  router.push('/');
  setTimeout(() => {
    window.location.reload();
  }, 50);
};
</script>

<template>
  <div class="navbar navbar-expand-lg">
    <div class="container">
      <div class="d-flex align-items-center">
        <h2 class="navbar__title">Sticker Shop</h2>
        <RouterLink to="/" class="nav-link fs-4">Home</RouterLink>
      </div>
      <div class="icons">
        <template v-if="isLoggedIn">
          <RouterLink to="/account" class="nav-link fs-4">
            <FontAwesomeIcon icon="user-circle"/>
          </RouterLink>
          <a @click.prevent="logoutButton" href="#" class="nav-link fs-4">
            <FontAwesomeIcon icon="sign-out-alt"/>
          </a>
        </template>
        <template v-else>
          <RouterLink to="/signup" class="nav-link fs-4">
            <FontAwesomeIcon icon="user-plus"/>
          </RouterLink>
          <RouterLink to="/login" class="nav-link fs-4">
            <FontAwesomeIcon icon="sign-in-alt"/>
          </RouterLink>
        </template>
        <RouterLink to="/cart" class="nav-link fs-4">
          <FontAwesomeIcon icon="cart-shopping"/>
        </RouterLink>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.navbar__title {
  margin-right: 32px;
}
.icons {
  display: flex;
  gap: 10px;
}
</style>
