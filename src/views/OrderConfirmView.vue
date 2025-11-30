<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { API_URL } from '@/config';
import CoreNavbar from '@/components/CoreNavbar.vue';

const route = useRoute();
const orderId = Number(route.params.orderId);

const loading = ref(true);
const order = ref(null);
const error = ref(null);

async function loadOrder() {
  try {
    const res = await fetch(`${API_URL}orders/${orderId}`);
    if (!res.ok) throw new Error("Order not found");

    order.value = await res.json();
  } catch (_) {
    error.value = "Failed to load order.";
  } finally {
    loading.value = false;
  }
}

onMounted(loadOrder);
</script>