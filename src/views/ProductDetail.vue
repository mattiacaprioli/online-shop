<template>
  <main class="h-screen">
    <button @click="router.push({ name: 'Catalog' })" class="capitalize font-semibold px-4 py-2 text-blue-900 rounded-md cursor-pointer hover:text-blue-700 active:text-blue-600">Back to catalog</button>
    <div class="flex flex-col sm:flex-row my-20">
      <div class="sm:mr-8">
        <img :src="selectedProduct.thumbnail" alt="" class="w-64 rounded-md">
      </div>
      <div class="mt-4 sm:mt-0">
        <p class="font-semibold text-xl">Brand: {{ selectedProduct.brand }}</p>
        <p class="text-gray-700">Description: {{ selectedProduct.description }}</p>
        <h2 class="font-bold text-2xl"> ${{ selectedProduct.price }}</h2>
        <button @click="addToCart" class="py-2 px-4 bg-green-500 text-white rounded hover:bg-green-600 cursor-pointer mt-4">Add to cart</button>
      </div>
    </div>
  </main>
</template>

<script>
import {defineComponent} from 'vue';

export default defineComponent({
    name: 'ProductDetails'
})
</script>

<script setup>
import {computed} from "vue";
import {productsStore} from "@/stores/products";
import {useRoute, useRouter} from "vue-router"

const store = productsStore()
const router = useRouter()
const route = useRoute()

const selectedProduct = computed(() => {
    return store.products.find((item) => item.id === Number(route.params.id)) 
})

const addToCart = () => {
    store.addToCart(selectedProduct.value)
    router.push({name: 'CartView'})
}
</script>

<style scoped>
</style>