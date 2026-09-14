<template>
  <div class="max-w-md mx-auto py-12 px-6 text-center space-y-6">
    <div class="w-16 h-16 rounded-2xl bg-[#4a7c59] text-white flex items-center justify-center mx-auto text-2xl font-bold font-serif shadow-md">
      A
    </div>
    <div class="space-y-2">
      <h1 class="text-3xl font-serif font-bold text-[#2e3230]">Anonly</h1>
      <p class="text-sm text-[#4a4e4a]">Platform pesan anonim aman dan terenkripsi.</p>
    </div>
    <div class="space-y-3 pt-4">
      <NuxtLink to="/dashboard" class="w-full py-3.5 px-4 rounded-xl bg-[#4a7c59] text-white font-bold text-sm shadow-sm block hover:opacity-95">
        Buka Kotak Masuk (Dashboard) 📥
      </NuxtLink>
      <NuxtLink to="/share" class="w-full py-3.5 px-4 rounded-xl bg-[#f0e8db] text-[#5e5548] font-bold text-sm shadow-sm block hover:bg-[#d4ccbf]">
        Bagi Tautan Profil 🔗
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'default' })
</script>
