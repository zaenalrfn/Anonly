<template>
  <nav class="fixed bottom-0 w-full z-50 bg-[#faf6f0]/85 backdrop-blur-xl shadow-[0_-2px_16px_rgba(46,50,48,0.06)]">
    <div class="flex justify-around items-center h-20 px-3 max-w-md mx-auto">
      <NuxtLink to="/dashboard" class="flex flex-col items-center gap-1 min-w-[72px]" :class="route.path.startsWith('/dashboard') ? 'text-[#4a7c59] font-bold' : 'text-[#4a4e4a]'">
        <span class="material-symbols-outlined text-[26px]">inbox</span>
        <span class="text-[11px]">Inbox</span>
      </NuxtLink>
      <NuxtLink to="/share" class="flex flex-col items-center gap-1 min-w-[72px]" :class="route.path.startsWith('/share') ? 'text-[#4a7c59] font-bold' : 'text-[#4a4e4a]'">
        <span class="material-symbols-outlined text-[26px]">share</span>
        <span class="text-[11px]">Bagi Link</span>
      </NuxtLink>
      <NuxtLink to="/profile" class="flex flex-col items-center gap-1 min-w-[72px]" :class="route.path.startsWith('/profile') ? 'text-[#4a7c59] font-bold' : 'text-[#4a4e4a]'">
        <span class="material-symbols-outlined text-[26px]">person</span>
        <span class="text-[11px]">Profil</span>
      </NuxtLink>
    </div>
  </nav>
</template>
<script setup>
const route = useRoute()
</script>
