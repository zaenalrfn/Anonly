<template>
  <article class="rounded-xl bg-white p-4 shadow-[0_4px_20px_rgba(46,50,48,0.06)]">
    <div class="flex items-start justify-between gap-3 mb-2.5">
      <div class="flex items-center gap-2">
        <span class="w-2.5 h-2.5 rounded-full bg-[#4a7c59] ring-4 ring-[#c8e8d0]/40"></span>
        <span class="text-[11px] font-bold text-[#4a7c59] uppercase">Pesan Baru</span>
      </div>
      <span class="text-[11px] text-[#4a4e4a]">{{ time }}</span>
    </div>
    <p class="text-[15px] font-medium leading-relaxed mb-3.5">“{{ content }}”</p>
    <div class="flex items-center justify-between pt-2">
      <NuxtLink :to="`/messages/${id}`" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-[#f0e8db] text-[#5e5548] text-xs font-bold">
        <span class="material-symbols-outlined text-[16px]">send_to_mobile</span>
        <span>Balas via Story</span>
      </NuxtLink>
      <div class="flex items-center gap-1 text-[#4a4e4a]">
        <button class="w-8 h-8 rounded-lg flex items-center justify-center hover:bg-[#f0ece4]"><span class="material-symbols-outlined text-[18px]">flag</span></button>
        <button class="w-8 h-8 rounded-lg flex items-center justify-center hover:bg-[#f0ece4] hover:text-[#b83230]"><span class="material-symbols-outlined text-[18px]">delete</span></button>
      </div>
    </div>
  </article>
</template>
<script setup>
defineProps({ id: { type: String, default: '1' }, content: { type: String, default: '' }, time: { type: String, default: '' } })
</script>
