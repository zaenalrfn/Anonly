<template>
  <div class="space-y-6 pb-20">
    <!-- Profile Bento Header -->
    <div class="bg-[#f0ece4] rounded-2xl p-6 shadow-sm relative overflow-hidden">
      <div class="absolute -right-8 -top-8 w-32 h-32 bg-[#4a7c59]/10 rounded-full blur-xl pointer-events-none"></div>
      <div class="flex items-center gap-4 relative z-10">
        <div class="relative">
          <div class="w-20 h-20 rounded-full overflow-hidden shadow-md bg-[#faf6f0]">
            <img src="https://lh3.googleusercontent.com/aida-public/AB6AXuCXjK8T9g_DE63sgQt8oUQ7HxrH96QRhH6mEKKgApjm0rLIW567yiqHH_mcUAwQVAv10VmP7md90HqaaOhgttPIqJT56pTPDCRfNaD5J27_EwLFABX6RGBqnwfy_MyV4NXjVCi1QzKxPuhOBluPBr_Vlh49ofdRg6PUFEgAEUK0jNUvkSNTJzHD8dm42mSsu-4bvhJuhn_t64Dx2Zx6m7bbHLkM7nMmvRpbuzjgN8jbMBCt76yZu4gI0A" alt="Clara Shinta" class="w-full h-full object-cover">
          </div>
          <span class="absolute bottom-0 right-0 w-6 h-6 rounded-full bg-[#4a7c59] text-white flex items-center justify-center shadow-sm">
            <span class="material-symbols-outlined text-[15px]">verified</span>
          </span>
        </div>
        <div class="flex-1 min-w-0">
          <h2 class="font-serif font-bold text-xl text-[#2e3230] truncate">Clara Shinta</h2>
          <p class="text-xs font-bold text-[#4a7c59]">@clarashinta</p>
          <p class="text-xs text-[#4a4e4a] truncate mt-0.5">clara.shinta@gmail.com</p>
        </div>
      </div>
    </div>

    <!-- Letterbox Stats Bento -->
    <div class="grid grid-cols-3 gap-2.5">
      <div class="bg-white p-4 rounded-xl text-center shadow-sm flex flex-col items-center border border-[#c4c8bc]/20">
        <div class="w-8 h-8 rounded-full bg-[#c8e8d0] text-[#2a6038] flex items-center justify-center mb-1">
          <span class="material-symbols-outlined text-base">mark_email_unread</span>
        </div>
        <span class="text-xl font-serif font-extrabold">18</span>
        <span class="text-[11px] text-[#4a4e4a] mt-0.5">Pesan Masuk</span>
      </div>
      <div class="bg-white p-4 rounded-xl text-center shadow-sm flex flex-col items-center border border-[#c4c8bc]/20">
        <div class="w-8 h-8 rounded-full bg-[#f0e8db] text-[#5e5548] flex items-center justify-center mb-1">
          <span class="material-symbols-outlined text-base">quickreply</span>
        </div>
        <span class="text-xl font-serif font-extrabold">8</span>
        <span class="text-[11px] text-[#4a4e4a] mt-0.5">Telah Dibalas</span>
      </div>
      <div class="bg-white p-4 rounded-xl text-center shadow-sm flex flex-col items-center border border-[#c4c8bc]/20">
        <div class="w-8 h-8 rounded-full bg-[#f8e0a8] text-[#554020] flex items-center justify-center mb-1">
          <span class="material-symbols-outlined text-base">shield</span>
        </div>
        <span class="text-xl font-serif font-extrabold">1</span>
        <span class="text-[11px] text-[#4a4e4a] mt-0.5">Disaring AI</span>
      </div>
    </div>

    <!-- Username Management -->
    <div class="bg-white rounded-2xl p-5 shadow-sm space-y-4 border border-[#c4c8bc]/20">
      <div class="flex items-center gap-2">
        <span class="material-symbols-outlined text-[#4a7c59] text-xl">link</span>
        <h3 class="font-serif font-bold text-base">Tautan & Username</h3>
      </div>
      <div>
        <label class="block text-xs font-semibold text-[#4a4e4a] mb-1.5">Username Akun</label>
        <div class="flex items-center bg-[#faf6f0] rounded-xl px-3 py-2.5 border border-[#c4c8bc]/40">
          <span class="text-xs font-bold text-[#6b6358] mr-1">anonly.id/u/</span>
          <input class="bg-transparent text-xs font-bold flex-1 outline-none cursor-not-allowed" disabled type="text" value="clarashinta">
          <span class="material-symbols-outlined text-base text-[#74796e]">lock</span>
        </div>
      </div>
      <div class="bg-[#f0ece4] p-3.5 rounded-xl space-y-2">
        <p class="text-xs font-bold">Cooldown Perubahan Username Aktif</p>
        <p class="text-[11px] text-[#4a4e4a]">Username dapat diubah maksimal 1x per 30 hari. Perubahan berikutnya pada 12 Oktober 2026.</p>
        <div class="w-full h-2 rounded-full bg-white overflow-hidden">
          <div class="bg-[#c4a66a] h-full rounded-full w-[20%]"></div>
        </div>
        <button class="w-full py-2 rounded-lg bg-[#e4e0d8] text-[#74796e] text-xs font-bold cursor-not-allowed" disabled>Ubah Username (Terkunci)</button>
      </div>
    </div>

    <!-- Security Toggles -->
    <div class="bg-white rounded-2xl p-5 shadow-sm space-y-4 border border-[#c4c8bc]/20">
      <div class="flex items-center gap-2">
        <span class="material-symbols-outlined text-[#4a7c59] text-xl">tune</span>
        <h3 class="font-serif font-bold text-base">Keamanan & Privasi Pesan</h3>
      </div>
      <div class="space-y-3">
        <div class="flex items-center justify-between p-3 rounded-xl bg-[#faf6f0]">
          <div>
            <span class="text-xs font-bold block">Menerima Pesan Baru</span>
            <span class="text-[11px] text-[#4a4e4a]">Kotak surat publik dapat menerima pesan</span>
          </div>
          <div class="w-12 h-7 rounded-full bg-[#4a7c59] p-1 flex items-center justify-end cursor-pointer">
            <div class="w-5 h-5 rounded-full bg-white shadow-sm"></div>
          </div>
        </div>
        <div class="flex items-center justify-between p-3 rounded-xl bg-[#faf6f0]">
          <div>
            <span class="text-xs font-bold block">Filter Ketat AI Terra Guard</span>
            <span class="text-[11px] text-[#4a4e4a]">Otomatis sembunyikan ujaran kebencian</span>
          </div>
          <div class="w-12 h-7 rounded-full bg-[#4a7c59] p-1 flex items-center justify-end cursor-pointer">
            <div class="w-5 h-5 rounded-full bg-white shadow-sm"></div>
          </div>
        </div>
      </div>
    </div>

    <!-- Legal & Logout -->
    <div class="bg-white rounded-2xl p-5 shadow-sm space-y-2 border border-[#c4c8bc]/20">
      <button @click="logout" class="w-full py-3 px-4 rounded-xl bg-[#f0ece4] text-[#6b6358] font-bold text-xs flex items-center justify-center gap-2">
        <span class="material-symbols-outlined text-base">logout</span>
        <span>Keluar Akun (Logout)</span>
      </button>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'default' })
const logout = () => {
  alert('Berhasil keluar akun!')
  navigateTo('/')
}
</script>
