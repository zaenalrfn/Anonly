<template>
  <div class="flex flex-col gap-3">
    <div class="flex items-center justify-between">
      <div class="flex items-baseline gap-2">
        <h1 class="text-xl font-serif font-bold">Pesan Rahasia</h1>
        <span class="text-xs font-semibold px-2 py-0.5 rounded-full bg-[#c8e8d0] text-[#002110]">{{ total }} Total</span>
      </div>
      <button class="flex items-center gap-1 text-xs font-semibold text-[#4a7c59]">
        <span class="material-symbols-outlined text-[16px]">done_all</span>
        <span>Tandai Dibaca</span>
      </button>
    </div>
    <div class="flex items-center gap-2 overflow-x-auto pb-1 text-xs">
      <button v-for="f in filters" :key="f.key" @click="$emit('filter', f.key)" :class="modelValue === f.key ? 'bg-[#4a7c59] text-white font-bold shadow-sm' : 'bg-[#f0ece4] text-[#4a4e4a] font-semibold'" class="shrink-0 px-3.5 py-1.5 rounded-full transition-all">{{ f.label }}</button>
    </div>
  </div>
</template>
<script setup>
defineProps({ total: { type: Number, default: 18 }, modelValue: { type: String, default: 'all' }, filters: { type: Array, default: () => [{ key: 'all', label: 'Semua (18)' }, { key: 'unread', label: 'Belum Dibaca (5)' }, { key: 'flagged', label: 'Di-flag (1)' }] } })
defineEmits(['filter', 'update:modelValue'])
</script>
