<template>
  <div class="space-y-5 pb-20">
    <!-- Toast -->
    <div v-if="toastMsg" class="fixed top-20 left-1/2 -translate-x-1/2 z-50 bg-[#2e3230] text-[#f5f0e8] px-4 py-2.5 rounded-full text-xs font-bold shadow-xl flex items-center gap-2.5 transition-all">
      <span class="material-symbols-outlined text-[20px] text-[#c8e8d0]">check_circle</span>
      <span>{{ toastMsg }}</span>
    </div>

    <!-- Hero Card: Link + QR Code -->
    <div class="relative overflow-hidden rounded-xl bg-[#4a7c59] text-white p-6 shadow-md">
      <div class="absolute -right-8 -bottom-10 w-44 h-44 rounded-full bg-[#78a886]/25 blur-xl pointer-events-none"></div>
      <div class="absolute -left-6 -top-8 w-36 h-36 rounded-full bg-[#c8e8d0]/20 blur-lg pointer-events-none"></div>
      <div class="relative z-10 flex flex-col space-y-4">
        <div class="flex items-center justify-between">
          <span class="text-[11px] font-extrabold tracking-widest uppercase text-[#d8f0de] bg-[#78a886]/40 px-3 py-1 rounded-full">Tautan Kotak Surat Kamu</span>
          <span class="material-symbols-outlined text-[#c8e8d0] text-[22px]">lock_open</span>
        </div>
        <div class="space-y-1">
          <p class="text-xs text-white/80 font-label">Tautan khusus profil kamu:</p>
          <div class="flex items-center justify-between bg-white/15 backdrop-blur-md rounded-xl px-3.5 py-2.5">
            <span class="text-base sm:text-lg font-bold font-headline tracking-wide text-white truncate">anonly.id/u/clarashinta</span>
            <button @click="copyLink" class="ml-2 p-1.5 rounded-lg bg-white/20 hover:bg-white/30 text-white transition-all active:scale-95">
              <span class="material-symbols-outlined text-[20px]">{{ copied ? 'check' : 'content_copy' }}</span>
            </button>
          </div>
        </div>
        <button @click="copyLink" class="w-full flex items-center justify-center gap-2 py-3 px-4 rounded-xl bg-white text-[#4a7c59] font-bold font-label text-sm shadow-sm active:scale-[0.98] transition-transform">
          <span class="material-symbols-outlined text-[20px]">link</span>
          <span>{{ copied ? 'Tersalin!' : 'Salin Tautan Lengkap' }}</span>
        </button>
        <!-- QR Code Section -->
        <div class="mt-2 pt-4 bg-white/10 backdrop-blur-sm rounded-xl p-4 flex items-center gap-4">
          <div class="w-20 h-20 rounded-xl bg-white p-2 flex-shrink-0 shadow-inner flex items-center justify-center">
            <svg class="w-full h-full text-[#2e3230]" fill="currentColor" viewBox="0 0 100 100">
              <rect height="30" rx="6" width="30" x="0" y="0"></rect>
              <rect fill="#ffffff" height="18" rx="3" width="18" x="6" y="6"></rect>
              <rect height="10" rx="2" width="10" x="10" y="10"></rect>
              <rect height="30" rx="6" width="30" x="70" y="0"></rect>
              <rect fill="#ffffff" height="18" rx="3" width="18" x="76" y="6"></rect>
              <rect height="10" rx="2" width="10" x="80" y="10"></rect>
              <rect height="30" rx="6" width="30" x="0" y="70"></rect>
              <rect fill="#ffffff" height="18" rx="3" width="18" x="6" y="76"></rect>
              <rect height="10" rx="2" width="10" x="10" y="80"></rect>
              <circle cx="45" cy="15" r="4"></circle>
              <circle cx="55" cy="22" r="3.5"></circle>
              <circle cx="40" cy="45" r="4.5"></circle>
              <circle cx="58" cy="45" r="4"></circle>
              <circle cx="50" cy="58" r="4"></circle>
              <circle cx="20" cy="45" r="4"></circle>
              <circle cx="80" cy="45" r="4"></circle>
              <circle cx="45" cy="80" r="4.5"></circle>
              <circle cx="65" cy="75" r="3.5"></circle>
              <circle cx="85" cy="85" r="4"></circle>
              <circle cx="75" cy="60" r="4"></circle>
            </svg>
          </div>
          <div class="flex-1 min-w-0 flex flex-col justify-between h-20">
            <div>
              <h2 class="text-sm font-bold font-headline leading-snug">QR Code Kotak Pesan</h2>
              <p class="text-[11px] text-white/80 font-label line-clamp-2 mt-0.5">Tunjukkan saat nongkrong langsung agar teman mudah scan.</p>
            </div>
            <button @click="showToast('QR Code disimpan ke galeri!')" class="inline-flex items-center gap-1.5 text-xs font-bold text-white bg-white/20 hover:bg-white/30 px-3 py-1.5 rounded-lg w-max transition-colors">
              <span class="material-symbols-outlined text-[16px]">file_download</span>
              Download QR
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Share Channels -->
    <div class="flex items-center justify-between pt-1">
      <div class="flex items-center gap-2">
        <span class="material-symbols-outlined text-[#4a7c59] text-[20px]">share</span>
        <h2 class="text-base font-bold font-headline">Bagikan Cepat</h2>
      </div>
      <span class="text-xs font-label text-[#6b6358]">Tingkatkan pesanmu</span>
    </div>

    <div class="flex flex-col space-y-3.5">
      <!-- Instagram Story -->
      <div class="p-4 rounded-xl bg-white shadow-sm flex flex-col space-y-3 border border-[#c4c8bc]/20">
        <div class="flex items-start justify-between">
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-xl bg-[#f8e0a8] flex items-center justify-center text-[#221a05] shadow-sm">
              <span class="material-symbols-outlined text-[24px]">photo_camera</span>
            </div>
            <div>
              <div class="flex items-center gap-2">
                <h3 class="text-sm font-bold font-headline">Instagram Story</h3>
                <span class="text-[10px] font-extrabold px-2 py-0.5 rounded-full bg-[#c4a66a] text-white font-label">Paling Populer</span>
              </div>
              <p class="text-xs text-[#4a4e4a] font-label">Panduan cepat 2 langkah</p>
            </div>
          </div>
        </div>
        <div class="rounded-lg bg-[#f0ece4] p-3 flex flex-col space-y-2 text-xs font-label text-[#4a4e4a]">
          <div class="flex items-center gap-2">
            <span class="w-4 h-4 rounded-full bg-[#4a7c59] text-white text-[10px] font-bold flex items-center justify-center flex-shrink-0">1</span>
            <span>Salin tautan kotak pesan kamu.</span>
          </div>
          <div class="flex items-center gap-2">
            <span class="w-4 h-4 rounded-full bg-[#4a7c59] text-white text-[10px] font-bold flex items-center justify-center flex-shrink-0">2</span>
            <span>Buka Instagram Story, pilih stiker <strong>"TAUTAN"</strong> &amp; tempel.</span>
          </div>
        </div>
        <button @click="copyLink(); showToast('Tautan siap ditempel di IG Story!')" class="w-full py-2.5 px-4 rounded-xl bg-[#4a7c59] text-white font-bold text-xs flex items-center justify-center gap-2 shadow-sm">
          <span class="material-symbols-outlined text-[18px]">photo_camera</span>
          <span>Buka Instagram Story</span>
        </button>
      </div>

      <!-- WhatsApp -->
      <div class="p-4 rounded-xl bg-white shadow-sm flex items-center justify-between border border-[#c4c8bc]/20">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-xl bg-[#c8e8d0] flex items-center justify-center text-[#002110] shadow-sm">
            <span class="material-symbols-outlined text-[24px]">chat</span>
          </div>
          <div>
            <h3 class="text-sm font-bold font-headline">WhatsApp Status / Chat</h3>
            <p class="text-xs text-[#4a4e4a] font-label">Kirim langsung ke kontak</p>
          </div>
        </div>
        <button @click="shareWA" class="py-2 px-3.5 rounded-lg bg-[#4a7c59] text-white font-bold text-xs">Share</button>
      </div>

      <!-- Social Media Bio -->
      <div class="p-4 rounded-xl bg-white shadow-sm flex items-center justify-between border border-[#c4c8bc]/20">
        <div class="flex items-center gap-3">
          <div class="w-10 h-10 rounded-xl bg-[#e4e0d8] flex items-center justify-center text-[#2e3230] shadow-sm">
            <span class="material-symbols-outlined text-[24px]">link</span>
          </div>
          <div>
            <h3 class="text-sm font-bold font-headline">Bio / Media Sosial</h3>
            <p class="text-xs text-[#4a4e4a] font-label">Tempel di bio profil</p>
          </div>
        </div>
        <button @click="copyLink(); showToast('Tautan disalin untuk Bio profil!')" class="py-2 px-3.5 rounded-lg bg-[#f0e8db] text-[#5e5548] font-bold text-xs">Salin</button>
      </div>
    </div>

    <!-- Promo Template -->
    <div class="bg-[#f5f1ea] rounded-xl p-4 space-y-3">
      <h3 class="text-xs font-bold font-headline uppercase tracking-wider text-[#6b6358]">Template Ajakan</h3>
      <p class="text-xs text-[#4a4e4a] leading-relaxed">"Klik link ini buat kirim pesan anonim ke aku! Jangan malu-malu ya 🤫 &rarr; anonly.id/u/clarashinta"</p>
      <button @click="copyTemplate" class="w-full py-2 px-3 rounded-lg bg-white text-[#4a7c59] font-bold text-xs flex items-center justify-center gap-1.5 shadow-sm">
        <span class="material-symbols-outlined text-[16px]">content_copy</span>
        <span>Salin Template</span>
      </button>
    </div>

    <!-- Footer -->
    <div class="text-center pt-2">
      <p class="text-[10px] text-[#74796e]">Anonly — Dibuat dengan cinta &amp; kejujuran</p>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'default' })

const copied = ref(false)
const toastMsg = ref('')

const showToast = (msg) => {
  toastMsg.value = msg
  setTimeout(() => toastMsg.value = '', 2600)
}

const copyLink = () => {
  navigator.clipboard.writeText('https://anonly.id/u/clarashinta')
  copied.value = true
  setTimeout(() => copied.value = false, 2200)
}

const copyTemplate = () => {
  navigator.clipboard.writeText('Klik link ini buat kirim pesan anonim ke aku! Jangan malu-malu ya 🤫 → anonly.id/u/clarashinta')
  showToast('Template ajakan berhasil disalin!')
}

const shareWA = () => {
  const text = encodeURIComponent('Klik link ini buat kirim pesan anonim ke aku! Jangan malu-malu ya 🤫 → anonly.id/u/clarashinta')
  window.open(`https://api.whatsapp.com/send?text=${text}`, '_blank')
}
</script>
