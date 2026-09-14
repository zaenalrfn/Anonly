<template>
  <div class="max-w-md mx-auto space-y-6 py-6 px-4">
    <!-- Recipient Header -->
    <div class="text-center space-y-3">
      <div class="w-20 h-20 rounded-full bg-[#78a886] mx-auto overflow-hidden shadow-md">
        <img src="https://lh3.googleusercontent.com/aida-public/AB6AXuCXjK8T9g_DE63sgQt8oUQ7HxrH96QRhH6mEKKgApjm0rLIW567yiqHH_mcUAwQVAv10VmP7md90HqaaOhgttPIqJT56pTPDCRfNaD5J27_EwLFABX6RGBqnwfy_MyV4NXjVCi1QzKxPuhOBluPBr_Vlh49ofdRg6PUFEgAEUK0jNUvkSNTJzHD8dm42mSsu-4bvhJuhn_t64Dx2Zx6m7bbHLkM7nMmvRpbuzjgN8jbMBCt76yZu4gI0A" alt="Clara Shinta" class="w-full h-full object-cover">
      </div>
      <div>
        <h1 class="text-xl font-bold font-serif">Kirim Pesan ke @{{ username }}</h1>
        <p class="text-xs text-[#4a4e4a] mt-1">Pesanmu terkirim secara 100% anonim dan terlindungi.</p>
      </div>
    </div>

    <!-- Message Form -->
    <div class="bg-white p-5 rounded-2xl shadow-sm border border-[#c4c8bc]/20 space-y-4">
      <textarea 
        v-model="message"
        rows="4" 
        maxlength="500"
        placeholder="Tulis pesan rahasiamu di sini..."
        class="w-full p-3 rounded-xl bg-[#faf6f0] border border-[#c4c8bc]/40 focus:outline-none focus:ring-2 focus:ring-[#4a7c59] text-sm resize-none"
      ></textarea>
      
      <div class="flex justify-between items-center text-xs text-[#4a4e4a]">
        <span>{{ message.length }}/500 karakter</span>
        <span class="text-emerald-700 font-semibold">🔒 Enkripsi Aktif</span>
      </div>

      <!-- Turnstile Simulation Box -->
      <div class="p-3 bg-[#f5f1ea] rounded-xl flex items-center justify-between text-xs border border-[#c4c8bc]/30">
        <div class="flex items-center gap-2">
          <input type="checkbox" id="turnstile" class="rounded accent-[#4a7c59]" checked disabled>
          <label for="turnstile">Cloudflare Turnstile Verified</label>
        </div>
        <span class="text-[10px] text-gray-500">Protected</span>
      </div>

      <button 
        @click="sendMessage"
        :disabled="!message.trim()"
        class="w-full py-3 px-4 rounded-xl bg-[#4a7c59] text-white font-bold text-sm shadow-sm hover:opacity-90 disabled:opacity-50 transition-opacity"
      >
        Kirim Pesan Rahasia 🚀
      </button>
    </div>
  </div>
</template>

<script setup>
definePageMeta({ layout: 'default' })
const route = useRoute()
const username = computed(() => route.params.username || 'clarashinta')
const message = ref('')

const sendMessage = () => {
  alert('Pesan anonim berhasil dikirim secara aman!')
  message.value = ''
}
</script>
