<script setup lang="ts">
    import { API_URL } from '@/config';
    import { onBeforeMount, ref } from 'vue';

    const orders = ref([]);
    const accountId = localStorage.getItem('account_id');
    
    onBeforeMount(async () => {
        const url = `${API_URL}orders/${accountId}/all`

        try {
            const res = await fetch(url)

            if (res.status !== 200) {
                return alert('Error fetching orders')
            }

            const data = await res.json()
            orders.value = data;
        } catch (error) {
            console.log(error)
        }
    });
</script>

<template>
    <main>
        <div class="container">
            <h2>Customer Orders</h2>
            <div class="row gy-4">
                <div v-for="order in orders" :key="order.order_id" class="col-12 mb-3 p-3 border rounded">
                    <!-- Insert order details here; Waiting on order component -->
                </div>
            </div>
        </div>
    </main>
</template>