<template>
  <Banner />
  <main>
    <ul class='flex flex-col md:flex-row justify-evenly  md:justify-center items-center '>
      <li @click="filterProducts('all')" class='btn'>All</li>
      <li @click="filterProducts('smartphones')" class='btn'>Smartphones</li>
      <li @click="filterProducts('laptops')" class='btn'>Laptops</li>
    </ul>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 my-8">
      <div
        class="bg-white rounded shadow-md transform hover:scale-105 cursor-pointer transition-transform"
        v-for="product in filteredProducts"
        :key="product.id"
        @click="goToProductPage(product.id)"
      >
        <img :src="product.thumbnail" alt="" class="w-full rounded-t-md h-36 bg-cover bg-center">
        <div class="p-4">
          <h2 class="font-semibold text-xl mb-2">{{ product.brand }}</h2>
          <p class="text-gray-700 text-sm mb-4">{{ product.description }}</p>
          <p class="font-bold text-lg">$ {{ product.price }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'CatalogView',
});
</script>

<script setup>
import { onMounted, computed, ref } from 'vue';
import { productsStore } from '@/stores/products';
import { useRouter } from 'vue-router';

import Banner from "@/components/Banner.vue";

const store = productsStore();
const router = useRouter();
const selectedCategory = ref('all');

const goToProductPage = (id) => {
  router.push({ name: 'productView', params: { id } });
};

onMounted(async () => {
  await store.fetchProductsFromDB();
});

const filteredProducts = computed(() => {
  if (selectedCategory.value === 'all') {
    return store.products.filter(
      (product) => product.category === 'smartphones' || product.category === 'laptops'
    );
  } else {
    return store.products.filter((product) => product.category === selectedCategory.value);
  }
});

const filterProducts = (category) => {
  selectedCategory.value = category;
};
</script>

<style scoped>
.btn {
  @apply capitalize font-semibold px-4 py-2 text-blue-900 rounded-md cursor-pointer hover:text-blue-700 focus:outline-none focus:ring active:text-blue-600;
}
</style>
