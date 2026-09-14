<template>
  <div class="min-h-screen flex flex-col pt-safe pb-safe">
    <main class="flex-1 px-4 space-y-5">
      <!-- Welcome Card -->
      <div class="bg-white rounded-xl p-5 shadow-sm relative overflow-hidden text-center">
        <div class="absolute -right-6 -bottom-6 w-24 h-24 bg-[#c8e8d0]/20 rounded-full blur-xl pointer-events-none"></div>
        <div class="w-14 h-14 mx-auto mb-3.5 bg-[#f0ece4] rounded-2xl flex items-center justify-center shadow-sm">
          <div class="w-9 h-9 rounded-xl bg-[#4a7c59] text-white flex items-center justify-center font-bold font-serif text-xl">A</div>
        </div>
        <h2 class="font-headline text-2xl font-bold tracking-tight leading-snug">Mulai Terima Pesan Anonimmu</h2>
        <p class="text-sm text-[#4a4e4a] mt-2 leading-relaxed">Daftar dalam 10 detik, bagikan tautanmu ke bio dan story sosial mediamu.</p>
      </div>

      <!-- Social Auth + Form -->
      <div class="bg-white rounded-xl p-5 shadow-sm space-y-4">
        <!-- Google Auth -->
        <button class="w-full flex items-center justify-center gap-3 bg-[#f0ece4] hover:bg-[#e4e0d8] active:scale-[0.99] font-headline font-semibold text-sm py-3.5 px-4 rounded-xl transition-all duration-200">
          <svg class="w-5 h-5" viewBox="0 0 24 24">
            <path d="M12 5c1.6 0 3 .6 4.1 1.6l3.1-3.1C17.3 1.7 14.8 1 12 1 7.5 1 3.7 3.6 1.9 7.3l3.7 2.9C6.5 7.4 9 5 12 5z" fill="#EA4335"></path>
            <path d="M23.5 12.3c0-.8-.1-1.6-.2-2.3H12v4.6h6.5c-.3 1.5-1.2 2.8-2.5 3.6l3.8 3c2.2-2 3.7-5.1 3.7-8.9z" fill="#4285F4"></path>
            <path d="M5.6 14.8c-.2-.7-.4-1.5-.4-2.8 0-1.3.2-2.1.4-2.8L1.9 6.3C.7 8.7 0 10.3 0 12s.7 3.3 1.9 5.7l3.7-2.9z" fill="#FBBC05"></path>
            <path d="M12 23c3.2 0 6-1.1 8-3l-3.8-3c-1.1.7-2.5 1.2-4.2 1.2-3 0-5.5-2-6.4-4.8L1.9 16.3C3.7 20.4 7.5 23 12 23z" fill="#34A853"></path>
          </svg>
          <span>Lanjutkan dengan Google</span>
        </button>

        <!-- Separator -->
        <div class="relative flex items-center justify-center my-5">
          <div class="w-full h-px bg-[#c4c8bc]"></div>
          <span class="absolute bg-white px-3 font-label text-xs font-semibold text-[#6b6358] uppercase tracking-wider">atau daftar dengan email</span>
        </div>

        <!-- Form -->
        <form class="space-y-4">
          <!-- Username -->
          <div>
            <div class="flex items-center justify-between mb-1.5">
              <label class="font-headline font-semibold text-xs" for="username">Pilih Username Link</label>
              <span v-if="usernameAvailable" class="text-[11px] font-label font-bold text-[#4a7c59] flex items-center gap-1 bg-[#c8e8d0]/35 px-2 py-0.5 rounded-full">
                <span class="material-symbols-outlined text-xs">check_circle</span>
                Username tersedia!
              </span>
            </div>
            <div class="flex items-center bg-[#f5f1ea] rounded-xl px-3.5 py-2.5 focus-within:bg-[#e4e0d8] transition-colors">
              <span class="font-label text-sm text-[#6b6358] font-medium tracking-tight">anonly.id/u/</span>
              <input v-model="username" @input="checkUsername" class="w-full bg-transparent font-headline font-semibold text-sm focus:outline-none pl-1" placeholder="username-anda" type="text">
              <span class="material-symbols-outlined text-[#4a7c59] text-xl ml-1" v-if="usernameAvailable">verified</span>
            </div>
            <p class="mt-1 text-[11px] text-[#6b6358] font-label">Tautan publik untuk disematkan di Instagram, TikTok, & Twitter.</p>
          </div>

          <!-- Email -->
          <div>
            <label class="block font-headline font-semibold text-xs mb-1.5" for="email">Alamat Email Aktif</label>
            <div class="flex items-center bg-[#f5f1ea] rounded-xl px-3.5 py-2.5 focus-within:bg-[#e4e0d8] transition-colors">
              <span class="material-symbols-outlined text-[#6b6358] text-lg mr-2">mail</span>
              <input v-model="email" class="w-full bg-transparent text-sm focus:outline-none" placeholder="nama@email.com" type="email">
            </div>
          </div>

          <!-- Password -->
          <div>
            <label class="block font-headline font-semibold text-xs mb-1.5" for="password">Kata Sandi</label>
            <div class="flex items-center bg-[#f5f1ea] rounded-xl px-3.5 py-2.5 focus-within:bg-[#e4e0d8] transition-colors">
              <span class="material-symbols-outlined text-[#6b6358] text-lg mr-2">lock</span>
              <input v-model="password" :type="showPassword ? 'text' : 'password'" class="w-full bg-transparent text-sm focus:outline-none tracking-wider" placeholder="Minimal 8 karakter">
              <button @click="showPassword = !showPassword" class="text-[#6b6358] hover:text-[#2e3230] p-1">
                <span class="material-symbols-outlined text-lg">{{ showPassword ? 'visibility' : 'visibility_off' }}</span>
              </button>
            </div>
          </div>

          <!-- Cooldown Info -->
          <div class="bg-[#f0e8db]/50 rounded-xl p-3.5 flex items-start gap-3">
            <span class="material-symbols-outlined text-[#c4a66a] text-lg shrink-0 mt-0.5">info</span>
            <div class="text-[12px] text-[#5e5548] leading-relaxed">
              <span class="font-bold">Aturan Penggantian Username:</span> Username dapat diubah maksimal <strong>1x setiap 30 hari</strong> untuk mencegah perebutan ID dan memvalidasi keaslian tautan temanmu.
            </div>
          </div>

          <!-- Submit -->
          <button type="button" @click="register" class="w-full bg-[#4a7c59] hover:bg-[#4a7c59]/95 text-white font-headline font-bold text-sm py-3.5 px-4 rounded-xl shadow-[0_6px_20px_rgba(74,124,89,0.28)] flex items-center justify-center gap-2 transition-all active:scale-[0.99] mt-2">
            <span>Buat Akun & Dapatkan Link</span>
            <span class="text-base">🎁</span>
          </button>
        </form>
      </div>

      <!-- Footer -->
      <div class="text-center px-4 space-y-2">
        <div class="flex items-center justify-center gap-2 text-[#6b6358] text-xs font-label">
          <span class="material-symbols-outlined text-sm text-[#4a7c59]">security</span>
          <span>Enkripsi privasi pesan & perlindungan data 100% aman</span>
        </div>
        <p class="text-[11px] text-[#6b6358] leading-relaxed">
          Dengan mendaftar, kamu menyetujui <a class="font-semibold text-[#4a7c59] underline underline-offset-2" href="#">Syarat & Ketentuan</a> serta <a class="font-semibold text-[#4a7c59] underline underline-offset-2" href="#">Kebijakan Privasi</a> Anonly.
        </p>
      </div>
    </main>

    <nav class="fixed bottom-0 w-full z-50 pb-safe bg-[#faf6f0]/85 backdrop-blur-xl shadow-[0_-2px_16px_rgba(46,50,48,0.06)]">
      <div class="flex justify-around items-center h-20 px-3">
        <NuxtLink to="/dashboard" class="flex flex-col items-center gap-1 min-w-[72px] h-14 rounded-xl text-[#4a4e4a] transition-colors">
          <span class="material-symbols-outlined text-[26px]">inbox</span>
          <span class="text-[11px]">Inbox</span>
        </NuxtLink>
        <NuxtLink to="/share" class="flex flex-col items-center gap-1 min-w-[72px] h-14 rounded-xl text-[#4a4e4a] transition-colors">
          <span class="material-symbols-outlined text-[26px]">share</span>
          <span class="text-[11px]">Bagi Link</span>
        </NuxtLink>
        <NuxtLink to="/profile" class="flex flex-col items-center gap-1 min-w-[72px] h-14 rounded-xl text-[#4a7c59] font-bold transition-colors">
          <span class="material-symbols-outlined text-[26px]">person</span>
          <span class="text-[11px]">Profil</span>
        </NuxtLink>
      </div>
    </nav>
  </div>
</template>

<script setup>
definePageMeta({ layout: false })

const username = ref('clarashinta')
const email = ref('clara.shinta@gmail.com')
const password = ref('')
const showPassword = ref(false)
const usernameAvailable = ref(true)

const checkUsername = () => {
  usernameAvailable.value = username.value.length >= 3 && !username.value.includes(' ')
}

const register = () => {
  alert('Akun berhasil dibuat! Redirect ke dashboard...')
  navigateTo('/dashboard')
}
</script>