<script setup lang="ts">
const lists = [
  {
    step: 1,
    title: 'Ariza topshirish',
    description: `O'qish bo'yicha arizangizni topshiring va qo'ng'iroq kuting`,
    icon: 'M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z',
  },
  {
    step: 2,
    title: 'Guruh tashkil etish',
    description: "Yetarli o'quvchi yig'ilganda guruh tashkil etiladi va dars jadvali belgilanadi",
    icon: 'M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z',
  },
  {
    step: 3,
    title: 'Darslar boshlanadi',
    description: "Ayollar va erkaklar uchun alohida guruhlarda professional o'qituvchilar bilan",
    icon: 'M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.246 18 16.5 18c-1.746 0-3.332.477-4.5 1.253',
  },
]
</script>

<template>
  <section class="py-24 bg-[var(--bg-primary)]">
    <div class="max-w-7xl mx-auto px-6">
      <!-- Header -->
      <div class="text-center mb-20">
        <div
          class="inline-flex items-center px-4 py-2 bg-[var(--accent)]/10 text-[var(--accent)] rounded-full text-sm font-medium mb-4"
        >
          Qadamma-qadam Jarayon
        </div>
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-6">Biz qanday ishlaymiz?</h2>
        <p class="text-lg text-[var(--text-secondary)] max-w-3xl mx-auto">
          Sizning Qur'on o'rganish safari bo'yicha oddiy va tushunarli yo'l xaritasi
        </p>
      </div>

      <!-- Steps Grid -->
      <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
        <div
          v-for="list in lists"
          :key="list.step"
          class="bg-white p-8 rounded-lg border border-[var(--border-color)] hover:border-[var(--accent)] hover:shadow-xl hover:-translate-y-1 transition-all duration-300 text-center group"
        >
          <!-- Step Number -->
          <div class="mb-6">
            <div
              class="w-16 h-16 bg-[var(--primary)] rounded-full flex items-center justify-center text-white font-bold text-2xl mx-auto shadow-lg group-hover:bg-[var(--accent)] group-hover:scale-110 transition-all duration-300"
            >
              {{ list.step }}
            </div>
          </div>

          <!-- Content -->
          <div>
            <h3
              class="text-xl font-bold text-[var(--text-primary)] mb-4 group-hover:text-[var(--accent)] transition-colors duration-300"
            >
              {{ list.title }}
            </h3>
            <p class="text-[var(--text-secondary)] leading-relaxed">
              {{ list.description }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
