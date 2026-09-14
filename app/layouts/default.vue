<template>
  <div class="min-h-screen flex flex-col bg-[#faf6f0] text-[#2e3230]">
    <AppHeader :title="headerTitle" :statusText="headerStatus" />
    <main class="flex-1 flex flex-col relative w-full pt-20 pb-24 px-4 max-w-2xl mx-auto">
      <slot />
    </main>
    <BottomNav />
  </div>
</template>
<script setup>
import AppHeader from '~/components/layout/AppHeader.vue'
import BottomNav from '~/components/layout/BottomNav.vue'

const route = useRoute()
const headerTitle = computed(() => {
  if (route.path.includes('share')) return 'Bagi Link'
  if (route.path.includes('profile')) return 'Profil Akun'
  if (route.path.includes('messages')) return 'Detail Pesan'
  return 'Kotak Masuk'
})
const headerStatus = computed(() => route.path.includes('u/') ? 'Kirim Pesan' : 'Siap Terima Pesan')
</script>
