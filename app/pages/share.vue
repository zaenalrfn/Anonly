<template>
  <div class="space-y-6">
    <div class="relative overflow-hidden rounded-xl bg-[#4a7c59] text-white p-6 shadow-md">
      <div class="relative z-10 space-y-4">
        <span class="text-[11px] font-extrabold uppercase bg-white/20 px-3 py-1 rounded-full">Tautan Kotak Surat Kamu</span>
        <div>
          <p class="text-xs text-white/80">Tautan khusus profil kamu:</p>
          <div class="flex items-center justify-between bg-white/15 backdrop-blur-md rounded-xl px-3.5 py-2.5 mt-1">
            <span class="text-base font-bold font-serif truncate">anonly.id/u/clarashinta</span>
            <button @click="copy" class="p-1.5 rounded-lg bg-white/20 hover:bg-white/30 text-white">
              <span class="material-symbols-outlined text-[20px]">content_copy</span>
            </button>
          </div>
        </div>
        <button @click="copy" class="w-full py-3 px-4 rounded-xl bg-white text-[#4a7c59] font-bold text-sm shadow-sm">
          Salin Tautan Lengkap
        </button>
      </div>
    </div>

    <!-- Share Channels -->
    <div class="space-y-3.5">
      <h2 class="text-base font-bold font-serif">Bagikan Cepat</h2>
      
      <!-- Instagram Story -->
      <div class="p-4 rounded-xl bg-white shadow-sm space-y-3 border border-[#c4c8bc]/20">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-xl bg-[#f8e0a8] flex items-center justify-center text-[#221a05]">
            <span class="material-symbols-outlined text-[24px]">photo_camera</span>
          </div>
          <div>
            <h3 class="text-sm font-bold font-serif">Instagram Story</h3>
            <p class="text-xs text-[#4a4e4a]">Panduan cepat pasang stiker link</p>
          </div>
        </div>
        <button class="w-full py-2.5 px-4 rounded-xl bg-[#c4a66a] text-white font-bold text-xs flex items-center justify-center gap-2">
          Buka Instagram Story
        </button>
      </div>

      <!-- WhatsApp -->
      <div class="p-4 rounded-xl bg-white shadow-sm flex items-center justify-between border border-[#c4c8bc]/20">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-xl bg-[#c8e8d0] flex items-center justify-center text-[#002110]">
            <span class="material-symbols-outlined text-[24px]">chat</span>
          </div>
          <div>
            <h3 class="text-sm font-bold font-serif">WhatsApp Status / Chat</h3>
            <p class="text-xs text-[#4a4e4a]">Kirim langsung ke kontak</p>
          </div>
        </div>
        <button class="py-2 px-3.5 rounded-lg bg-[#4a7c59] text-white font-bold text-xs">Share</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const copy = () => navigator.clipboard.writeText('https://anonly.id/u/clarashinta')
</script>
