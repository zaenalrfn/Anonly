<template>
  <div class="max-w-md mx-auto space-y-6 pb-12">
    <!-- Top Action Row -->
    <div class="flex items-center justify-between">
      <NuxtLink to="/dashboard" class="inline-flex items-center gap-1 text-sm font-semibold text-[#4a7c59]">
        <span class="material-symbols-outlined text-[18px]">arrow_back_ios</span>
        <span>Kembali ke Inbox</span>
      </NuxtLink>
    </div>

    <!-- Story Card Studio (9:16 Adaptive Frame) -->
    <StoryCardStudio 
      question="Jujur sebenernya gue udah naksir lo dari semester 2 tapi gak berani ngomong langsung haha 🙈" 
      :reply="replyText" 
    />

    <!-- Reply Customizer Input -->
    <div class="flex flex-col gap-2 bg-white p-4 rounded-2xl shadow-sm border border-[#c4c8bc]/20">
      <label class="text-xs font-bold uppercase tracking-wider text-[#4a4e4a] flex items-center gap-1.5">
        <span class="material-symbols-outlined text-[16px] text-[#4a7c59]">edit_note</span>
        <span>Tulis Balasanmu</span>
      </label>
      <textarea 
        v-model="replyText"
        rows="2"
        maxlength="120"
        placeholder="Tulis balasanmu di sini..."
        class="w-full rounded-xl bg-[#faf6f0] p-3 text-sm text-[#2e3230] border border-[#c4c8bc]/40 focus:outline-none focus:ring-2 focus:ring-[#4a7c59] resize-none"
      ></textarea>
      <div class="flex justify-between text-[11px] text-[#4a4e4a]">
        <span>Teks otomatis diperbarui di kartu story</span>
        <span>{{ replyText.length }}/120</span>
      </div>
    </div>

    <!-- Export Actions -->
    <div class="space-y-3">
      <button @click="exportIG" class="w-full h-14 rounded-2xl bg-[#4a7c59] text-white font-bold text-sm flex items-center justify-center gap-2 shadow-md">
        <span class="material-symbols-outlined text-xl">photo_camera</span>
        <span>Export ke Instagram Story</span>
      </button>
      <button @click="exportWA" class="w-full h-13 py-3.5 rounded-2xl bg-[#f0e8db] text-[#5e5548] font-semibold text-sm flex items-center justify-center gap-2 shadow-sm">
        <span class="material-symbols-outlined text-xl">share</span>
        <span>Salin Gambar & Link WhatsApp</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import StoryCardStudio from '~/components/story/StoryCardStudio.vue'

const route = useRoute()
const replyText = ref('Waduh siapa nih haha, reveal diri dong di DM 😂')

const exportIG = () => {
  alert('Membuka Instagram Story editor...')
}

const exportWA = () => {
  navigator.clipboard.writeText(`Balasan Anonly: "${replyText.value}" -> https://anonly.id/u/clarashinta`)
  alert('Tautan & balasan berhasil disalin untuk WhatsApp!')
}
</script>
