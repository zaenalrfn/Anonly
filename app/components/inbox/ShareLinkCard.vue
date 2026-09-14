<template>
  <div class="relative overflow-hidden rounded-xl bg-gradient-to-br from-[#4a7c59] via-[#416f4f] to-[#365c42] p-5 text-white shadow-[0_8px_24px_rgba(74,124,89,0.18)]">
    <div class="relative z-10 flex flex-col gap-4">
      <div class="flex items-start justify-between gap-2">
        <div class="flex flex-col">
          <span class="text-[11px] uppercase tracking-wider font-bold text-[#c8e8d0]">Tautan Kotak Suratmu</span>
          <h2 class="text-base font-serif font-bold mt-0.5">anonly.id/u/clarashinta</h2>
        </div>
        <div class="w-9 h-9 rounded-full bg-white/15 flex items-center justify-center shrink-0">
          <span class="material-symbols-outlined text-[#c8e8d0] text-xl">qr_code_2</span>
        </div>
      </div>
      <p class="text-xs text-[#d8f0de] leading-relaxed">Tempel tautan ini di bio atau stiker IG Story biar temanmu bisa kirim rahasia anonim!</p>
      <div class="grid grid-cols-2 gap-2.5 pt-1">
        <button @click="copied = true; $emit('copy')" class="flex items-center justify-center gap-2 py-2.5 px-3 rounded-lg bg-white text-[#2e3230] font-bold text-xs shadow-sm active:scale-95 transition-transform">
          <span class="material-symbols-outlined text-[18px] text-[#4a7c59]">{{ copied ? 'check' : 'content_copy' }}</span>
          <span>{{ copied ? 'Tersalin!' : 'Salin Tautan' }}</span>
        </button>
        <NuxtLink to="/share" class="flex items-center justify-center gap-1.5 py-2.5 px-3 rounded-lg bg-[#f8e0a8] text-[#221a05] font-bold text-xs shadow-sm active:scale-95 transition-transform">
          <span class="material-symbols-outlined text-[18px]">photo_camera</span>
          <span>Share ke IG</span>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>
<script setup>
const copied = ref(false)
defineEmits(['copy'])
</script>
