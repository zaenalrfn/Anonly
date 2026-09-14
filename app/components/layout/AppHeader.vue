<template>
  <header class="fixed top-0 w-full z-50 pt-safe bg-[#faf6f0]/80 backdrop-blur-xl shadow-[0_1px_8px_rgba(46,50,48,0.04)]">
    <div class="h-16 px-4 flex items-center justify-between gap-3">
      <div class="flex items-center gap-2.5 min-w-0">
        <div class="w-8 h-8 rounded-xl bg-[#4a7c59] text-white flex items-center justify-center font-bold">A</div>
        <div class="flex flex-col min-w-0">
          <span class="text-sm font-bold font-serif tracking-tight leading-none">Anonly</span>
          <div class="flex items-center gap-1.5 mt-0.5">
            <span class="w-2 h-2 rounded-full bg-[#4a7c59] inline-block"></span>
            <span class="text-[11px] font-semibold text-[#4a7c59] truncate">{{ statusText }}</span>
          </div>
        </div>
      </div>
      <div class="flex items-center gap-2">
        <span class="text-xs font-serif font-semibold text-[#6b6358] px-2.5 py-1 rounded-full bg-[#f0e8db]/60 truncate max-w-[120px]">{{ title }}</span>
        <img alt="Profile" class="w-8 h-8 rounded-full object-cover" src="https://lh3.googleusercontent.com/aida-public/AB6AXuCXjK8T9g_DE63sgQt8oUQ7HxrH96QRhH6mEKKgApjm0rLIW567yiqHH_mcUAwQVAv10VmP7md90HqaaOhgttPIqJT56pTPDCRfNaD5J27_EwLFABX6RGBqnwfy_MyV4NXjVCi1QzKxPuhOBluPBr_Vlh49ofdRg6PUFEgAEUK0jNUvkSNTJzHD8dm42mSsu-4bvhJuhn_t64Dx2Zx6m7bbHLkM7nMmvRpbuzjgN8jbMBCt76yZu4gI0A">
      </div>
    </div>
  </header>
</template>
<script setup>
defineProps({ title: { type: String, default: 'Kotak Masuk' }, statusText: { type: String, default: 'Siap Terima Pesan' } })
</script>
