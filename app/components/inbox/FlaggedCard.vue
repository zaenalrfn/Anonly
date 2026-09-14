<template>
  <article class="rounded-xl bg-[#f5f1ea] p-4 shadow-sm">
    <div class="flex items-start justify-between gap-3 mb-2.5">
      <div class="flex items-center gap-1.5 px-2 py-0.5 rounded-md bg-[#f8e0a8] text-[#221a05]">
        <span class="material-symbols-outlined text-[14px]">warning</span>
        <span class="text-[10px] font-bold uppercase">Berpotensi Sensitif</span>
      </div>
      <span class="text-[11px] text-[#4a4e4a]">{{ time }}</span>
    </div>
    <div class="mb-3.5 bg-[#f0ece4]/60 p-3 rounded-lg">
      <p class="text-[14px] blur-[2.5px] hover:blur-none transition-all cursor-pointer select-none">“{{ content }}”</p>
      <span class="block text-[10px] text-[#4a4e4a] mt-1.5 italic">Pesan disaring otomatis sistem AI Terra Guard.</span>
    </div>
    <div class="flex items-center justify-between gap-2">
      <button class="inline-flex items-center gap-1.5 px-2.5 py-1.5 rounded-lg bg-[#e4e0d8] text-xs font-semibold"><span class="material-symbols-outlined text-[16px]">policy</span><span>Buka Laporan</span></button>
      <button class="inline-flex items-center gap-1 px-2.5 py-1.5 rounded-lg bg-[#ffdad8] text-[#690005] text-xs font-bold"><span class="material-symbols-outlined text-[16px]">delete_forever</span><span>Hapus Permanen</span></button>
    </div>
  </article>
</template>
<script setup>
defineProps({ content: { type: String, default: '' }, time: { type: String, default: '' } })
</script>
