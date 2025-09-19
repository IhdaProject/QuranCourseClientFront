<script setup lang="ts">
// Hero section interactivity
const scrollToMap = () => {
  const mapSection = document.querySelector('#map-section')
  if (mapSection) {
    mapSection.scrollIntoView({ behavior: 'smooth' })
  }
}

const scrollToAbout = () => {
  const aboutSection = document.querySelector('#about')
  if (aboutSection) {
    aboutSection.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>
<template>
  <!-- Hero Section -->
  <section
    class="relative min-h-[90vh] flex items-center justify-center bg-gradient-to-br from-[var(--primary-dark)] via-[var(--primary)] to-[var(--primary-light)] overflow-hidden"
  >
    <!-- Simple Background Overlay -->
    <div class="absolute inset-0 bg-black/10"></div>

    <!-- Content -->
    <div class="relative z-10 max-w-7xl mx-auto px-6 py-20 text-center">
      <div class="space-y-12">
        <!-- Badge -->
        <div
          class="inline-flex items-center px-6 py-3 bg-white/10 backdrop-blur-sm rounded-full border border-white/20"
        >
          <span class="text-white font-medium">🎓 #1 Qur'on Ta'lim Markazi</span>
        </div>

        <!-- Main Content -->
        <div class="space-y-6">
          <h1 class="text-4xl md:text-6xl lg:text-7xl font-bold text-white leading-tight">
            Qur'onni
            <span class="text-[var(--accent)]">Professional</span>
            <br />Darajada O'rganing
          </h1>
          <p class="text-xl md:text-2xl text-gray-200 max-w-4xl mx-auto leading-relaxed">
            Tajribali ustozlar rahbarligida Qur'oni Karimni to'g'ri va tartibli o'rganish uchun
            <span class="text-[var(--accent)] font-semibold">zamonaviy</span> ta'lim tizimi
          </p>
        </div>

        <!-- CTA Buttons -->
        <div class="flex flex-col sm:flex-row gap-4 justify-center items-center max-w-lg mx-auto">
          <button
            @click="scrollToMap"
            class="w-full sm:w-auto px-8 py-4 bg-[var(--accent)] hover:bg-[var(--accent)]/90 text-[var(--primary-dark)] font-bold text-lg rounded-lg shadow-lg hover:shadow-xl transform hover:-translate-y-1 transition-all duration-300"
          >
            <span class="flex items-center justify-center gap-2">
              <svg
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M13 10V3L4 14h7v7l9-11h-7z"
                />
              </svg>
              Kursga Yozilish
            </span>
          </button>

          <button
            @click="scrollToAbout"
            class="w-full sm:w-auto px-8 py-4 bg-white/10 hover:bg-white/20 backdrop-blur-sm border-2 border-white/30 hover:border-white/50 text-white font-semibold text-lg rounded-lg transition-all duration-300"
          >
            <span class="flex items-center justify-center gap-2">
              <svg
                class="w-5 h-5"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                />
              </svg>
              Batafsil Ma'lumot
            </span>
          </button>
        </div>

        <!-- Stats -->
        <div class="grid grid-cols-2 md:grid-cols-4 gap-6 max-w-4xl mx-auto pt-12">
          <div class="text-center space-y-2">
            <div class="text-3xl md:text-4xl font-bold text-white">1500+</div>
            <div class="text-sm md:text-base text-gray-300">Faol Talabalar</div>
          </div>
          <div class="text-center space-y-2">
            <div class="text-3xl md:text-4xl font-bold text-white">50+</div>
            <div class="text-sm md:text-base text-gray-300">Professional Ustozlar</div>
          </div>
          <div class="text-center space-y-2">
            <div class="text-3xl md:text-4xl font-bold text-white">15+</div>
            <div class="text-sm md:text-base text-gray-300">Yillik Tajriba</div>
          </div>
          <div class="text-center space-y-2">
            <div class="text-3xl md:text-4xl font-bold text-white">98%</div>
            <div class="text-sm md:text-base text-gray-300">Muvaffaqiyat</div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
