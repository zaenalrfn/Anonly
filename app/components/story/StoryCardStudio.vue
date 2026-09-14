<template>
  <div class="flex flex-col items-center">
    <div class="w-full aspect-[9/14] rounded-3xl bg-gradient-to-b from-[#f0ece4] via-[#f5f1ea] to-[#e8e2d5] p-5 flex flex-col justify-between relative overflow-hidden shadow-lg">
      <div class="relative z-10 flex items-center justify-between">
        <div class="flex items-center gap-2 bg-white/80 px-3 py-1.5 rounded-full shadow-sm">
          <span class="text-xs font-semibold">anonly</span>
        </div>
        <div class="bg-white/70 px-2.5 py-1 rounded-full text-[11px] font-medium flex items-center gap-1">
          <span class="material-symbols-outlined text-[14px] text-[#4a7c59]">lock</span>
          <span>Pesan Anonim</span>
        </div>
      </div>
      <div class="relative z-10 flex flex-col items-center gap-4 my-auto px-2">
        <div class="w-full bg-white rounded-2xl p-5 shadow-sm relative">
          <p class="font-serif font-semibold text-lg text-center leading-snug pt-1">"{{ question }}"</p>
        </div>
        <div class="w-full bg-[#78a886]/25 rounded-2xl p-4 shadow-sm">
          <div class="flex items-center gap-1.5 mb-1.5">
            <span class="w-2 h-2 rounded-full bg-[#4a7c59] animate-pulse"></span>
            <span class="text-[11px] font-bold uppercase tracking-wider text-[#4a7c59]">Balasan Kamu</span>
          </div>
          <p class="text-sm font-semibold italic leading-relaxed">{{ reply }}</p>
        </div>
      </div>
      <div class="relative z-10 flex items-center justify-between pt-2">
        <div class="flex items-center gap-1.5 bg-white/90 px-3.5 py-1.5 rounded-full shadow-sm">
          <span class="material-symbols-outlined text-[15px] text-[#c4a66a]">link</span>
          <span class="text-xs font-semibold">anonly.id/u/clarashinta</span>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
defineProps({ question: { type: String, default: '' }, reply: { type: String, default: '' } })
</script>
