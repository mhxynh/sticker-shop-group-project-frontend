<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { API_URL } from '@/config';

const route = useRoute();
const orderId = route.params.orderId;

const order = ref();
 
async function loadOrder() {
  const accountId = localStorage.getItem('account_id');
  try {
    const res = await fetch(`${API_URL}orders/${orderId}/${accountId}`);
    if (!res.ok) {
      alert("Failed to fetch order");
    };
    order.value = await res.json();
  } catch {
    console.log("Failed to load order");
  }
}

onMounted(loadOrder);
</script>

<template>
  <div class="container">
    <h1>Order Confirmation</h1>
    <div v-if="order">
      <p><strong>Order ID:</strong> {{ order.order_id }}</p>
      <p><strong>Account ID:</strong> {{ order.account_id }}</p>

      <h3 class="mt-3">Items</h3>
      <ul>
        <li v-for="item in order.items" :key="item.id">
          Sticker ID: {{ item.sticker_id }},
          Material ID: {{ item.sticker_material_id }},
          Size ID: {{ item.sticker_size_id }}
        </li>
      </ul>
    </div>
    <p v-else class="text-danger">Failed to load order</p>
  </div>
</template>
