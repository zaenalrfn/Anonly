<template>
  <div class="space-y-6 pb-20">
    <!-- Status Bar -->
    <div class="flex items-center justify-between px-4 py-2.5 rounded-2xl bg-[#f5f1ea] border border-[#c4c8bc]/30 shadow-sm">
      <div class="flex items-center gap-2.5">
        <span class="relative flex h-2.5 w-2.5">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[#4a7c59] opacity-75"></span>
          <span class="relative inline-flex rounded-full h-2.5 w-2.5 bg-[#4a7c59]"></span>
        </span>
        <span class="text-xs font-bold text-[#4a7c59]">Realtime sync aktif</span>
        <span class="text-[11px] text-[#4a4e4a]">· Firestore tersambung</span>
      </div>
      <span class="material-symbols-outlined text-[18px] text-[#4a4e4a] cursor-pointer hover:text-[#4a7c59]">sync</span>
    </div>

    <!-- Quick Share Bento Card -->
    <ShareLinkCard @copy="showToast('Tautan berhasil disalin!')" />

    <!-- Inbox Filter & Header -->
    <InboxFilter v-model="currentFilter" :total="18" @filter="currentFilter = $event" />

    <!-- Messages Feed -->
    <div class="flex flex-col space-y-3.5">
      <MessageCard 
        id="1" 
        content="Jujur sebenernya gue udah naksir lo dari semester 2 tapi gak berani ngomong langsung haha 🙈" 
        time="5 menit lalu" 
      />
      
      <MessageCard 
        id="2" 
        content="Kira-kira kapan mau resign dari kantor yang sekarang? Spill dong tips interviewnya!" 
        time="42 menit lalu" 
      />

      <FlaggedCard 
        content="Kenapa sih sombong banget sekarang ga pernah nongkrong bareng lagi..." 
        time="3 jam lalu" 
      />

      <article class="rounded-xl bg-white/80 p-4 shadow-sm border border-[#c4c8bc]/20 opacity-95">
        <div class="flex items-start justify-between gap-3 mb-2">
          <div class="flex items-center gap-1.5 text-[#4a4e4a]">
            <span class="material-symbols-outlined text-[16px]">drafts</span>
            <span class="text-[11px] font-semibold tracking-wide">Sudah Dibaca</span>
          </div>
          <span class="text-[11px] text-[#4a4e4a]/70">Kemarin, 19:20</span>
        </div>
        <p class="text-[15px] font-medium leading-relaxed mb-3">“Semangat skripsinya kak Clara! Pasti bisa lulus tahun ini 🎓✨”</p>
        <div class="flex items-center justify-between pt-1">
          <NuxtLink to="/messages/1" class="inline-flex items-center gap-1.5 px-3 py-1.5 rounded-lg bg-[#f0e8db]/70 text-[#5e5548] text-xs font-bold">
            <span class="material-symbols-outlined text-[16px]">send_to_mobile</span>
            <span>Balas Lagi</span>
          </NuxtLink>
          <div class="flex items-center gap-1 text-[#4a4e4a]">
            <button class="w-8 h-8 rounded-lg flex items-center justify-center hover:bg-[#f0ece4]"><span class="material-symbols-outlined text-[18px]">bookmark_border</span></button>
            <button class="w-8 h-8 rounded-lg flex items-center justify-center hover:bg-[#f0ece4] hover:text-[#b83230]"><span class="material-symbols-outlined text-[18px]">delete</span></button>
          </div>
        </div>
      </article>
    </div>

    <!-- Footer Notice -->
    <div class="flex flex-col items-center justify-center py-6 px-4 text-center space-y-2">
      <div class="w-10 h-10 rounded-full bg-[#f0ece4] flex items-center justify-center text-[#6b6358]">
        <span class="material-symbols-outlined text-xl">spa</span>
      </div>
      <p class="text-xs font-serif text-[#6b6358] italic">Kamu telah membaca semua rahasia terbaru hari ini.</p>
    </div>

    <!-- Toast Notification -->
    <div v-if="toastMsg" class="fixed bottom-24 left-1/2 -translate-x-1/2 z-50 bg-[#2e3230] text-[#f5f0e8] px-4 py-2.5 rounded-full text-xs font-bold shadow-xl flex items-center gap-2">
      <span class="material-symbols-outlined text-base text-[#8ecf9e]">check_circle</span>
      <span>{{ toastMsg }}</span>
    </div>
  </div>
</template>

<script setup>
import ShareLinkCard from '~/components/inbox/ShareLinkCard.vue'
import InboxFilter from '~/components/inbox/InboxFilter.vue'
import MessageCard from '~/components/inbox/MessageCard.vue'
import FlaggedCard from '~/components/inbox/FlaggedCard.vue'

definePageMeta({ layout: 'default' })
const currentFilter = ref('all')
const toastMsg = ref('')

const showToast = (msg) => {
  toastMsg.value = msg
  setTimeout(() => toastMsg.value = '', 2500)
}
</script>
