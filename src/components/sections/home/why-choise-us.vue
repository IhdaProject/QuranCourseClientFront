<script setup lang="ts">
import Icon from '@/components/common/Icon.vue'

const features = [
  {
    icon: 'Building2',
    title: 'Davlat Ruxsati',
    description:
      "Davlat tasarrufidagi diniy qo'mita qoshida rasmiy ruxsat berilgan va ro'yxatdan o'tgan madrasa",
  },
  {
    icon: 'Users',
    title: 'Qulay Guruhlar',
    description:
      'Ayollar va erkaklar uchun alohida guruhlar hamda yoshga mos sinflar tashkil etiladi',
  },
  {
    icon: 'GraduationCap',
    title: 'Professional Ustozlar',
    description:
      "Malakali va ko'p yillik tajribaga ega bo'lgan professional o'qituvchilar bilan sifatli ta'lim",
  },
  {
    icon: 'BookOpen',
    title: "Sifatli Ta'lim",
    description: "Zamonaviy va an'anaviy metodlarni birlashtirgan holda offline ta'lim tizimi",
  },
]
</script>

<template>
  <section id="about" class="py-24 bg-[var(--primary-bg)]">
    <div class="max-w-7xl mx-auto px-6">
      <!-- Header -->
      <div class="text-center mb-20">
        <div
          class="inline-flex items-center px-4 py-2 bg-[var(--accent)]/10 text-[var(--accent)] rounded-full text-sm font-medium mb-4"
        >
          Bizning Afzalliklarimiz
        </div>
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-6">
          Nima uchun bizni tanlaysiz?
        </h2>
        <p class="text-lg text-[var(--text-secondary)] max-w-3xl mx-auto">
          Professional ta'lim va sifatli xizmat ko'rsatish orqali eng yaxshi natijalarni
          kafolatlaymiz
        </p>
      </div>

      <!-- Features Grid - Modern 2025 Layout -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
        <div
          v-for="(feature, index) in features"
          :key="index"
          class="bg-white p-8 rounded-lg border border-[var(--border-color)] hover:border-[var(--accent)] hover:shadow-xl hover:-translate-y-1 transition-all duration-300 group"
        >
          <!-- Icon -->
          <div class="mb-6">
            <div
              class="w-16 h-16 bg-[var(--primary)] rounded-lg flex items-center justify-center group-hover:bg-[var(--accent)] group-hover:scale-110 transition-all duration-300"
            >
              <Icon :name="feature.icon" :size="28" class="text-white" />
            </div>
          </div>

          <!-- Content -->
          <div>
            <h3
              class="text-xl font-bold text-[var(--text-primary)] mb-4 group-hover:text-[var(--accent)] transition-colors duration-300"
            >
              {{ feature.title }}
            </h3>
            <p class="text-[var(--text-secondary)] leading-relaxed">
              {{ feature.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
