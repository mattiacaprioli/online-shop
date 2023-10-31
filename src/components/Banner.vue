<template>
    <div class="relative bg-left">
      <img :src="banner" alt="" class="w-full h-72 sm:h-60 object-cover bg-bottom" />
      <div class="absolute inset-0 flex items-center justify-center text-white text-2xl font-semibold bg-black bg-opacity-50">
        <h1>Find the Perfect Device for You</h1>
      </div>
    </div>
  </template>
  
<script>
  import banner from '../assets/images/banner.jpg'

  export default {
    name: 'Banner',
    data(){
        return{
            banner: banner,
        }
    }
  };
</script>
  
<style scoped>
</style>
  