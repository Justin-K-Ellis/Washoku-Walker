<script setup>
import { onMounted, watch } from 'vue'
import { RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue'
import { useBrowserLocationStore } from './stores/browserLoc'
import useGetLocation from './composablies/useGetLocation'

onMounted(() => {
  let browserLocStore = useBrowserLocationStore()
  const { latitude, longitude, locationShared } = useGetLocation()

  watch(locationShared, (shared) => {
    if (shared) {
      browserLocStore.latitude = latitude.value
      browserLocStore.longitude = longitude.value
    } else {
      console.warn('no loc data')
    }
  })
})
</script>

<template>
  <Navbar />
  <div class="gap-8 w-9/10 md:w-6/10 mx-auto mt-4 md:mt-32">
    <RouterView />
  </div>
</template>
