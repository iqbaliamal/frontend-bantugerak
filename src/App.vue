<template>
  <div class="flex flex-col w-full min-h-screen bg-gray-100">
    
    <!-- Header -->
    <Header />

    <!-- content -->
    <router-view></router-view>

    <!-- footer -->
    <Footer />

  </div>
</template>

<script>

  import Header from '@/components/Header.vue'
  import Footer from '@/components/Footer.vue'

  export default {
    components: {
      Header,
      Footer,
    }
  }
</script>

<style>

</style>