<template>
  <main class="max-h-[100vh] overflow-auto min-h-[100vh]">
    <button @click="router.push({ name: 'Catalog' })" class="capitalize font-semibold px-4 py-2 text-blue-900 rounded-md cursor-pointer hover:text-blue-700">Back to catalog</button>
    <div v-if="!store.cart.length" class="text-center mt-8">
      <h1 class="text-2xl font-bold mt-20">Empty Cart...</h1>
    </div>
    <div v-else>
      <div v-for="item in store.cart" :key="item.id" class="my-6 p-4 rounded shadow-lg bg-slate-50">
        <div class="flex flex-col gap-8 sm:flex-row justify-between items-center">
          <img :src="item.thumbnail" alt="" class="w-60 sm:w-32 rounded-md">
          <div>
            <span class="font-semibold mr-2">Brand: {{ item.brand }}</span>
            <span class="text-gray-700 mr-2">Category: {{ item.category }}</span>
            <span class="font-bold text-lg">$ {{ item.price }}</span>
            
          </div>
          <button @click="removeFromCart(item.id)" class="capitalize font-semibold px-4 py-2 text-red-700 rounded-md cursor-pointer hover:text-red-900">Remove</button>
        </div>
      </div>
    </div>
  </main>
</template>

  

<script>
import {defineComponent} from 'vue';

export default defineComponent({
    name: 'CartView'
})
</script>

<script setup>
import {productsStore} from "@/stores/products";
import {useRouter} from "vue-router";

const router = useRouter()

const store = productsStore()

const removeFromCart = (id) => {
    store.removeFromCart(id)
}

</script>

<style scoped>
</style>