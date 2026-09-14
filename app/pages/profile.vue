<template>
  <div class="space-y-4 pb-20">
    <!-- Profile Card -->
    <div class="bg-[#f0ece4] rounded-2xl p-5 shadow-sm relative overflow-hidden">
      <div class="absolute -right-8 -top-8 w-32 h-32 bg-[#4a7c59]/10 rounded-full blur-xl pointer-events-none"></div>
      <div class="flex flex-col sm:flex-row sm:items-center gap-4 relative z-10">
        <div class="relative self-start sm:self-center">
          <div class="w-20 h-20 rounded-full overflow-hidden shadow-sm bg-[#e4e0d8]">
            <img src="https://lh3.googleusercontent.com/aida-public/AB6AXuCXjK8T9g_DE63sgQt8oUQ7HxrH96QRhH6mEKKgApjm0rLIW567yiqHH_mcUAwQVAv10VmP7md90HqaaOhgttPIqJT56pTPDCRfNaD5J27_EwLFABX6RGBqnwfy_MyV4NXjVCi1QzKxPuhOBluPBr_Vlh49ofdRg6PUFEgAEUK0jNUvkSNTJzHD8dm42mSsu-4bvhJuhn_t64Dx2Zx6m7bbHLkM7nMmvRpbuzjgN8jbMBCt76yZu4gI0A" alt="Clara Shinta" class="w-full h-full object-cover">
          </div>
          <span class="absolute bottom-0 right-0 w-6 h-6 rounded-full bg-[#4a7c59] text-white flex items-center justify-center shadow-sm">
            <span class="material-symbols-outlined text-[15px]">verified</span>
          </span>
        </div>
        <div class="flex-1 min-w-0">
          <div class="flex items-center gap-1.5">
            <h2 class="font-headline font-bold text-xl text-[#2e3230] truncate">Clara Shinta</h2>
          </div>
          <p class="text-xs font-bold text-[#4a7c59] tracking-wide">@clarashinta</p>
          <div class="flex items-center gap-1.5 mt-1 text-[#4a4e4a] text-xs truncate">
            <span class="material-symbols-outlined text-[15px] text-[#c4a66a]">mail</span>
            <span class="truncate">clara.shinta@gmail.com</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Stats Bento -->
    <div class="grid grid-cols-3 gap-2.5">
      <div class="bg-[#f0ece4] p-3.5 rounded-xl text-center shadow-sm flex flex-col items-center">
        <div class="w-8 h-8 rounded-full bg-[#c8e8d0] text-[#2a6038] flex items-center justify-center mb-1">
          <span class="material-symbols-outlined text-base">mark_email_unread</span>
        </div>
        <span class="text-xl font-headline font-extrabold">18</span>
        <span class="text-[11px] text-[#4a4e4a] mt-0.5">Pesan Masuk</span>
      </div>
      <div class="bg-[#f0ece4] p-3.5 rounded-xl text-center shadow-sm flex flex-col items-center">
        <div class="w-8 h-8 rounded-full bg-[#f0e8db] text-[#5e5548] flex items-center justify-center mb-1">
          <span class="material-symbols-outlined text-base">quickreply</span>
        </div>
        <span class="text-xl font-headline font-extrabold">8</span>
        <span class="text-[11px] text-[#4a4e4a] mt-0.5">Telah Dibalas</span>
      </div>
      <div class="bg-[#f0ece4] p-3.5 rounded-xl text-center shadow-sm flex flex-col items-center">
        <div class="w-8 h-8 rounded-full bg-[#f8e0a8] text-[#554020] flex items-center justify-center mb-1">
          <span class="material-symbols-outlined text-base">shield</span>
        </div>
        <span class="text-xl font-headline font-extrabold">1</span>
        <span class="text-[11px] text-[#4a4e4a] mt-0.5">Disaring AI</span>
      </div>
    </div>

    <!-- Username Management -->
    <div class="bg-[#f0ece4] rounded-xl p-5 shadow-sm space-y-3.5">
      <div class="flex items-center gap-2">
        <span class="material-symbols-outlined text-[#4a7c59] text-xl">link</span>
        <h3 class="font-headline font-bold text-base">Tautan &amp; Username</h3>
      </div>
      <div>
        <label class="block text-xs font-semibold text-[#4a4e4a] mb-1.5">Username Akun</label>
        <div class="flex items-center bg-[#faf6f0] rounded-lg px-3 py-2.5 shadow-inner">
          <span class="text-xs font-bold text-[#6b6358] mr-1">anonly.id/u/</span>
          <input class="bg-transparent text-xs font-bold flex-1 outline-none cursor-not-allowed opacity-85" disabled type="text" value="clarashinta">
          <span class="material-symbols-outlined text-base text-[#74796e]">lock</span>
        </div>
      </div>
      <div class="bg-[#f0ece4] p-3.5 rounded-lg space-y-2">
        <div class="flex items-start gap-2.5">
          <span class="material-symbols-outlined text-[#c4a66a] text-lg mt-0.5">history_toggle_off</span>
          <div>
            <p class="text-xs font-bold">Cooldown Perubahan Username Aktif</p>
            <p class="text-[11px] text-[#4a4e4a] mt-0.5">Username dapat diubah maksimal <strong>1x per 30 hari</strong>. Perubahan berikutnya pada <span class="font-semibold">12 Oktober 2026</span>.</p>
          </div>
        </div>
        <div class="space-y-1 pt-1">
          <div class="flex justify-between text-[10px] font-semibold text-[#4a4e4a]">
            <span>6 hari berlalu</span>
            <span class="text-[#c4a66a] font-bold">Sisa 24 hari lagi</span>
          </div>
          <div class="w-full h-2 rounded-full bg-[#faf6f0] overflow-hidden">
            <div class="bg-[#c4a66a] h-full rounded-full w-[20%]"></div>
          </div>
        </div>
        <button class="w-full mt-1 py-2 px-3 rounded-lg bg-[#e4e0d8] text-[#74796e] text-xs font-bold cursor-not-allowed" disabled>Ubah Username (Terkunci)</button>
      </div>
    </div>

    <!-- Security & Privacy -->
    <div class="bg-[#f0ece4] rounded-xl p-5 shadow-sm space-y-4">
      <div class="flex items-center gap-2">
        <span class="material-symbols-outlined text-[#4a7c59] text-xl">tune</span>
        <h3 class="font-headline font-bold text-base">Keamanan &amp; Privasi Pesan</h3>
      </div>
      <div class="space-y-3">
        <div class="flex items-center justify-between gap-3 p-3 rounded-lg bg-[#faf6f0]">
          <div>
            <div class="flex items-center gap-1.5">
              <span class="text-xs font-bold">Menerima Pesan Baru</span>
              <span class="px-1.5 py-0.5 rounded text-[9px] font-bold bg-[#c8e8d0] text-[#2a6038]">Aktif</span>
            </div>
            <p class="text-[11px] text-[#4a4e4a] mt-0.5">Kotak surat publik dapat menerima pesan</p>
          </div>
          <div class="w-12 h-7 rounded-full bg-[#4a7c59] p-1 flex-shrink-0">
            <div class="w-5 h-5 rounded-full bg-white shadow-sm translate-x-5"></div>
          </div>
        </div>
        <div class="flex items-center justify-between gap-3 p-3 rounded-lg bg-[#faf6f0]">
          <div>
            <div class="flex items-center gap-1.5">
              <span class="text-xs font-bold">Filter Ketat AI Terra Guard</span>
              <span class="px-1.5 py-0.5 rounded text-[9px] font-bold bg-[#c8e8d0] text-[#2a6038]">Aktif</span>
            </div>
            <p class="text-[11px] text-[#4a4e4a] mt-0.5">Otomatis sembunyikan ujaran kebencian</p>
          </div>
          <div class="w-12 h-7 rounded-full bg-[#4a7c59] p-1 flex-shrink-0">
            <div class="w-5 h-5 rounded-full bg-white shadow-sm translate-x-5"></div>
          </div>
        </div>
      </div>
      <div class="flex items-center gap-2.5 p-3 rounded-lg bg-[#f0ece4] text-[#5e5548]">
        <span class="material-symbols-outlined text-[#4a7c59] text-lg">verified_user</span>
        <span class="text-[11px] leading-tight"><strong>Enkripsi Satu Arah Aktif:</strong> Identitas dan jejak digital pengirim anonim 100% terjaga kerahasiaannya.</span>
      </div>
    </div>

    <!-- Help & Legal -->
    <div class="bg-[#f0ece4] rounded-xl p-5 shadow-sm space-y-2">
      <h3 class="font-headline font-bold text-xs uppercase tracking-wider text-[#6b6358] mb-2">Bantuan &amp; Ketentuan</h3>
      <a href="#" class="flex items-center justify-between py-2.5 px-3 rounded-lg hover:bg-[#faf6f0] transition-colors text-[#2e3230]">
        <div class="flex items-center gap-2.5">
          <span class="material-symbols-outlined text-[#6b6358] text-base">policy</span>
          <span class="text-xs font-semibold">Pedoman Komunitas &amp; Keamanan</span>
        </div>
        <span class="material-symbols-outlined text-[#74796e] text-sm">chevron_right</span>
      </a>
      <a href="#" class="flex items-center justify-between py-2.5 px-3 rounded-lg hover:bg-[#faf6f0] transition-colors text-[#2e3230]">
        <div class="flex items-center gap-2.5">
          <span class="material-symbols-outlined text-[#6b6358] text-base">privacy_tip</span>
          <span class="text-xs font-semibold">Kebijakan Privasi</span>
        </div>
        <span class="material-symbols-outlined text-[#74796e] text-sm">chevron_right</span>
      </a>
      <a href="#" class="flex items-center justify-between py-2.5 px-3 rounded-lg hover:bg-[#faf6f0] transition-colors text-[#2e3230]">
        <div class="flex items-center gap-2.5">
          <span class="material-symbols-outlined text-[#6b6358] text-base">description</span>
          <span class="text-xs font-semibold">Syarat &amp; Ketentuan</span>
        </div>
        <span class="material-symbols-outlined text-[#74796e] text-sm">chevron_right</span>
      </a>
      <div class="pt-4 mt-2 space-y-2.5">
        <button class="w-full py-3 px-4 rounded-lg bg-[#f0ece4] text-[#6b6358] font-bold text-xs hover:bg-[#e4e0d8] transition-colors flex items-center justify-center gap-2">
          <span class="material-symbols-outlined text-base">logout</span>
          <span>Keluar Akun (Logout)</span>
        </button>
        <button class="w-full py-2 px-3 text-center text-[#b83230] hover:text-[#690005] text-[11px] font-semibold transition-colors flex items-center justify-center gap-1 opacity-80 hover:opacity-100">
          <span class="material-symbols-outlined text-sm">delete_forever</span>
          <span>Hapus Akun Permanen</span>
        </button>
      </div>
    </div>
    <p class="text-[10px] text-center text-[#74796e] py-2">Anonly App v1.0.4 (Terra Edition) • Dibuat dengan cinta &amp; kejujuran</p>
  </div>
</template>
<script setup>definePageMeta({ layout: 'default' })</script>
