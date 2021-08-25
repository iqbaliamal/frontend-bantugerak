<template>
  <div>
    <!-- header -->
    <header>
      <div class="flex items-center bg-blue-800 justify-center fixed w-full h-14 px-4 z-40">
        <div class="w-full sm:max-w-lg mx-auto flex items-center justify-between h-full">
          <div class=" bg-white rounded-full h-10 w-11 p-1 mr-5 shadow-sm">
            <router-link :to="{name: 'home'}">
              <img src="@/assets/images/muslim.png" class="inline-block">
            </router-link>
          </div>
          <div class="relative w-full max-w-lg flex justify-end">
            <div class="absolute inset-y-0 flex items-center p-2 bg-gray-100 rounded-md">
              <svg class="w-4 h-4 text-right" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd"
                  d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                  clip-rule="evenodd"></path>
              </svg>
            </div>
            <input
              class="w-full h-8 pl-3 pr-8 text-sm text-gray-700 placeholder-gray-600 bg-gray-100 border-0 rounded-md dark:placeholder-gray-500 focus:placeholder-gray-500 focus:bg-white focus:border-purple-300 focus:outline-none focus:shadow-outline-purple form-input"
              type="text" @click="linkToSearch" v-model="search" @keyup="searchQuery" placeholder="Cari yang ingin kamu bantu" aria-label="Search" />
          </div>
        </div>
      </div>
    </header>
  </div>
</template>

<script>
  
//hook vue
  import { ref } from 'vue'
  
  //hook vue router
  import { useRouter } from 'vue-router'
  
  //hook vuex
  import { useStore } from 'vuex'
  
  export default {

    setup() {

      //router
      const router = useRouter()

      //store
      const store = useStore()

      //state seacrh
      const search = ref(null)

      //queryString
      function searchQuery() {
        store.dispatch('campaign/searchCampaign', search.value)
      }

      //redirect to route search
      function linkToSearch() {
        router.push({
          name: 'search'
        })
      }

      return {
        search,         // <-- state search
        linkToSearch,   // <-- method linkToSearch
        searchQuery     // <-- method searchQuery
      }
    }

  }
</script>

<style>

</style>