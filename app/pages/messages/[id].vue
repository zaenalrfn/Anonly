<template>
  <div class="space-y-6 pb-12">
    <div class="flex items-center justify-between">
      <NuxtLink to="/dashboard" class="inline-flex items-center gap-1 text-sm font-semibold text-[#4a7c59]">
        <span class="material-symbols-outlined text-[18px]">arrow_back_ios</span>
        <span>Kembali ke Inbox</span>
      </NuxtLink>
      <button @click="showMenu = !showMenu" class="w-9 h-9 rounded-full bg-[#f0ece4] flex items-center justify-center text-[#4a4e4a]">
        <span class="material-symbols-outlined text-[20px]">more_vert</span>
      </button>
    </div>

    <!-- Context Menu -->
    <div v-if="showMenu" class="flex flex-col gap-1 p-2 rounded-xl bg-white shadow-xl border border-[#c4c8bc]/30 max-w-xs ml-auto">
      <button @click="reportOpen = true; showMenu = false" class="w-full px-4 py-2.5 text-left text-sm font-medium text-[#b83230] flex items-center gap-2.5 hover:bg-[#ffdad8]/30 rounded-lg">
        <span class="material-symbols-outlined text-[18px]">flag</span>
        <span>Laporkan Pesan</span>
      </button>
      <button @click="deletedToast = true; setTimeout(() => navigateTo('/dashboard'), 800)" class="w-full px-4 py-2.5 text-left text-sm font-medium flex items-center gap-2.5 hover:bg-[#f0ece4] rounded-lg">
        <span class="material-symbols-outlined text-[18px]">delete</span>
        <span>Hapus Pesan</span>
      </button>
    </div>

    <StoryCardStudio :question="question" :reply="replyText" />

    <div class="flex flex-col gap-2">
      <div class="flex items-center justify-between px-1">
        <label class="text-xs font-bold uppercase tracking-wider text-[#4a4e4a] flex items-center gap-1.5">
          <span class="material-symbols-outlined text-[16px] text-[#4a7c59]">edit_note</span>
          <span>Tulis Balasanmu</span>
        </label>
        <span class="text-[11px] text-[#6b6358] font-medium">{{ replyText.length }} / 120</span>
      </div>
      <div class="relative">
        <textarea v-model="replyText" maxlength="120" rows="2" placeholder="Tulis balasanmu di sini..." class="w-full rounded-2xl bg-[#f0ece4] p-3.5 pr-10 text-sm text-[#2e3230] placeholder:text-[#6b6358] focus:outline-none focus:bg-white shadow-inner resize-none"></textarea>
        <button @click="replyText = ''" class="absolute right-3 top-3 text-[#6b6358] hover:text-[#2e3230] p-1">
          <span class="material-symbols-outlined text-[16px]">close</span>
        </button>
      </div>
      <p class="text-[11px] text-[#6b6358] px-1 flex items-center gap-1">
        <span class="material-symbols-outlined text-[13px]">info</span>
        <span>Teks otomatis diperbarui ke kartu pratinjau di atas.</span>
      </p>
    </div>

    <div class="flex flex-col gap-3">
      <button @click="showToast('Membuka Instagram Story editor...')" class="w-full h-14 rounded-2xl bg-[#4a7c59] text-white font-bold text-sm flex items-center justify-center gap-3 shadow-md">
        <span class="material-symbols-outlined text-xl">photo_camera</span>
        <span>Export ke Instagram Story</span>
      </button>
      <button @click="copyWA" class="w-full h-13 py-3.5 rounded-2xl bg-[#f0e8db] text-[#5e5548] font-semibold text-sm flex items-center justify-center gap-2.5 shadow-sm">
        <span class="material-symbols-outlined text-[20px]">share</span>
        <span>Salin Gambar &amp; Link WhatsApp</span>
      </button>
    </div>

    <div class="bg-[#f0ece4] rounded-xl p-3 flex items-start gap-2.5">
      <span class="material-symbols-outlined text-[#4a7c59] text-[18px] mt-0.5">verified_user</span>
      <p class="text-xs text-[#4a4e4a] leading-relaxed">Privasi pengirim dilindungi enkripsi satu arah. Hanya Anda yang dapat memutuskan untuk membagikan balasan ini ke publik.</p>
    </div>

    <!-- Report Modal (FR-12) 1:1 Stitch -->
    <div v-if="reportOpen" class="fixed inset-0 z-50 flex items-end sm:items-center justify-center p-0 sm:p-4 bg-[#2e3230]/40 backdrop-blur-sm">
      <div class="bg-white w-full max-w-md rounded-t-3xl sm:rounded-2xl p-6 shadow-2xl flex flex-col gap-4">
        <div class="flex items-center justify-between pb-2">
          <div class="flex items-center gap-2 text-[#b83230]">
            <span class="material-symbols-outlined text-[22px]">report_problem</span>
            <h2 class="font-headline font-bold text-base text-[#2e3230]">Laporkan Pesan</h2>
          </div>
          <button @click="reportOpen = false" class="w-8 h-8 rounded-full bg-[#f0ece4] flex items-center justify-center text-[#4a4e4a]">
            <span class="material-symbols-outlined text-[18px]">close</span>
          </button>
        </div>
        <p class="text-xs text-[#4a4e4a]">Bantu kami menjaga komunitas tetap aman. Pilih alasan pelaporan:</p>
        <div class="flex flex-col gap-2.5">
          <label v-for="o in reasons" :key="o.value" class="flex items-center gap-3 p-3 rounded-xl bg-[#f0ece4] hover:bg-[#e4e0d8] cursor-pointer">
            <input type="radio" :value="o.value" v-model="reportReason" class="w-4 h-4 accent-[#4a7c59]">
            <div>
              <span class="text-xs font-bold block">{{ o.label }}</span>
              <span class="text-[11px] text-[#6b6358]">{{ o.desc }}</span>
            </div>
          </label>
        </div>
        <div class="flex gap-2 mt-2">
          <button @click="reportOpen = false" class="flex-1 py-3 rounded-xl bg-[#f0ece4] text-[#2e3230] font-semibold text-xs">Batal</button>
          <button @click="reportOpen = false; showToast('Laporan berhasil dikirim. Terima kasih!')" class="flex-1 py-3 rounded-xl bg-[#b83230] text-white font-semibold text-xs shadow-sm">Kirim Laporan</button>
        </div>
      </div>
    </div>

    <!-- Toast -->
    <div v-if="toastMsg" class="fixed bottom-6 left-1/2 -translate-x-1/2 z-50 bg-[#2e3230] text-[#f5f0e8] px-4 py-2.5 rounded-full text-xs font-medium shadow-xl flex items-center gap-2">
      <span class="material-symbols-outlined text-[16px] text-[#8ecf9e]">check_circle</span>
      <span>{{ toastMsg }}</span>
    </div>
  </div>
</template>
<script setup>
import StoryCardStudio from '~/components/story/StoryCardStudio.vue'
const showMenu = ref(false)
const reportOpen = ref(false)
const reportReason = ref('bullying')
const toastMsg = ref('')
const deletedToast = ref(false)
const question = 'Jujur sebenernya gue udah naksir lo dari semester 2 tapi gak berani ngomong langsung haha 🙈'
const replyText = ref('Waduh siapa nih haha, reveal diri dong di DM 😂')
const reasons = [
  { value: 'bullying', label: 'Bullying & Pelecehan', desc: 'Pesan menghina, ancaman, atau merendahkan' },
  { value: 'hate_speech', label: 'Ujaran Kebencian', desc: 'Diskriminasi SARA atau ancaman kekerasan' },
  { value: 'spam_bot', label: 'Spam / Bot / Iklan', desc: 'Promosi link phishing, judi, atau pesan massal' }
]
const showToast = (m) => { toastMsg.value = m; setTimeout(() => toastMsg.value = '', 2600) }
const copyWA = () => {
  navigator.clipboard.writeText(`Pesan: "${question}" Balasan: "${replyText.value}" -> https://anonly.id/u/clarashinta`)
  showToast('Gambar & Link disalin untuk WhatsApp!')
}
</script>
