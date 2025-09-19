<script setup lang="ts">
import { ref, computed } from 'vue'
import BaseButton from '@/components/ui/BaseButton.vue'

const news = [
  {
    id: 1,
    title: 'Yangi filial Samarqandda ochildi',
    excerpt:
      "Samarqand shahrida 500 talaba sig'imli yangi o'quv markazimiz faoliyatini boshladi. Zamonaviy jihozlar va professional o'qituvchilar.",
    date: '2024-08-25',
    category: 'Yangiliklar',
    readTime: '3 daqiqa',
    image: '/api/placeholder/400/300',
    featured: true,
  },
  {
    id: 2,
    title: 'Onlayn Tajvid kurslari ishga tushdi',
    excerpt:
      'Endi siz uydan chiqmasdan ham professional Tajvid darslarini olishingiz mumkin. Barcha qurilmalarda ishlaydi.',
    date: '2024-08-20',
    category: "Ta'lim",
    readTime: '2 daqiqa',
    image: '/api/placeholder/400/300',
    featured: false,
  },
  {
    id: 3,
    title: "Xalqaro Qiroat musobaqasida g'alaba",
    excerpt:
      "Bizning talabamiz Xalqaro Qiroat musobaqasida 1-o'rinni egalladi. Ajoyib natija va o'qituvchilarimizning mehnati.",
    date: '2024-08-15',
    category: 'Muvaffaqiyat',
    readTime: '4 daqiqa',
    image: '/api/placeholder/400/300',
    featured: false,
  },
  {
    id: 4,
    title: 'Yangi Hifz dasturi ishga tushdi',
    excerpt:
      "Maxsus Hifz dasturi orqali talabalar 2 yil ichida to'liq Qur'oni Karimni yodlash imkoniyatiga ega bo'lishadi.",
    date: '2024-08-10',
    category: 'Dastur',
    readTime: '5 daqiqa',
    image: '/api/placeholder/400/300',
    featured: false,
  },
]

const categories = ['Barchasi', 'Yangiliklar', "Ta'lim", 'Muvaffaqiyat', 'Dastur']
const selectedCategory = ref('Barchasi')

const filteredNews = computed(() => {
  if (selectedCategory.value === 'Barchasi') {
    return news
  }
  return news.filter((item) => item.category === selectedCategory.value)
})

const formatDate = (dateStr: string) => {
  const date = new Date(dateStr)
  return date.toLocaleDateString('uz-UZ', {
    year: 'numeric',
    month: 'long',
    day: 'numeric',
  })
}
</script>

<template>
  <section class="bg-gray-50 py-20">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Header -->
      <div class="text-center mb-16">
        <h2 class="text-3xl font-bold text-gray-900 mb-4">Yangiliklar va E'lonlar</h2>
        <p class="text-gray-600 max-w-2xl mx-auto">
          O'quv markazimizning so'nggi yangiliklari va muhim e'lonlar bilan tanishing
        </p>
      </div>

      <!-- Category Filter -->
      <div class="flex flex-wrap justify-center gap-2 mb-12">
        <button
          v-for="category in categories"
          :key="category"
          @click="selectedCategory = category"
          :class="[
            'px-4 py-2 rounded-full text-sm font-medium transition-all duration-200',
            selectedCategory === category
              ? 'bg-gray-900 text-white'
              : 'bg-white border border-gray-200 text-gray-600 hover:bg-gray-50',
          ]"
        >
          {{ category }}
        </button>
      </div>

      <!-- News Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 gap-8">
        <!-- Featured Article (First Item) -->
        <article
          v-if="filteredNews[0] && filteredNews[0].featured"
          class="md:col-span-2 bg-white rounded-lg border border-gray-200 hover:shadow-sm transition-shadow overflow-hidden"
        >
          <div class="grid md:grid-cols-2 h-full">
            <!-- Image -->
            <div class="relative overflow-hidden bg-gray-100 h-64 md:h-auto">
              <div class="absolute inset-0 flex items-center justify-center">
                <svg
                  class="w-16 h-16 text-gray-400"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="1"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z"
                  />
                </svg>
              </div>
              <!-- Featured Badge -->
              <div class="absolute top-4 left-4">
                <span
                  class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-gray-900 text-white"
                >
                  <svg
                    class="w-4 h-4 mr-1"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"
                    />
                  </svg>
                  Asosiy
                </span>
              </div>
            </div>

            <!-- Content -->
            <div class="p-8 flex flex-col justify-between">
              <div>
                <div class="flex items-center gap-4 mb-4">
                  <span
                    class="inline-flex items-center px-3 py-1 rounded-full text-sm font-medium bg-[var(--primary-bg)] text-[var(--primary-dark)] border border-[var(--border-color)]"
                  >
                    {{ filteredNews[0].category }}
                  </span>
                  <span class="text-sm text-[var(--text-secondary)]">{{
                    formatDate(filteredNews[0].date)
                  }}</span>
                </div>

                <h3 class="text-xl font-bold text-gray-900 mb-4">
                  {{ filteredNews[0].title }}
                </h3>

                <p class="text-gray-600 mb-6 leading-relaxed">
                  {{ filteredNews[0].excerpt }}
                </p>
              </div>

              <div class="flex items-center justify-between">
                <BaseButton size="sm" variant="outline">
                  <svg
                    class="w-4 h-4 mr-2"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.246 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"
                    />
                  </svg>
                  Batafsil o'qish
                </BaseButton>
                <span class="text-sm text-[var(--text-secondary)]">{{
                  filteredNews[0].readTime
                }}</span>
              </div>
            </div>
          </div>
        </article>

        <!-- Regular Articles -->
        <article
          v-for="article in filteredNews.slice(filteredNews[0]?.featured ? 1 : 0)"
          :key="article.id"
          class="group bg-white border-l-4 border-[var(--warning-color)] hover:border-[var(--primary-dark)] rounded-lg shadow-sm hover:shadow-md transition-all duration-200 overflow-hidden"
        >
          <!-- Image -->
          <div class="relative overflow-hidden bg-[var(--primary-bg)] h-48">
            <div class="absolute inset-0 flex items-center justify-center">
              <svg
                class="w-12 h-12 text-[var(--text-secondary)]"
                fill="none"
                stroke="currentColor"
                stroke-width="1"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z"
                />
              </svg>
            </div>
          </div>

          <!-- Content -->
          <div class="p-6">
            <div class="flex items-center gap-3 mb-3">
              <span
                class="inline-flex items-center px-2 py-1 rounded-full text-xs font-medium bg-[var(--primary-bg)] text-[var(--primary-dark)] border border-[var(--border-color)]"
              >
                {{ article.category }}
              </span>
              <span class="text-xs text-[var(--text-secondary)]">{{
                formatDate(article.date)
              }}</span>
            </div>

            <h3
              class="heading-sm text-brand mb-3 group-hover:text-[var(--primary-light)] transition-colors duration-300 line-clamp-2"
            >
              {{ article.title }}
            </h3>

            <p class="body-sm text-[var(--text-secondary)] mb-4 leading-relaxed line-clamp-3">
              {{ article.excerpt }}
            </p>

            <div class="flex items-center justify-between">
              <BaseButton size="sm" variant="ghost">
                <svg
                  class="w-4 h-4 mr-2"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M17 8l4 4m0 0l-4 4m4-4H3"
                  />
                </svg>
                O'qish
              </BaseButton>
              <span class="text-xs text-[var(--text-secondary)]">{{ article.readTime }}</span>
            </div>
          </div>
        </article>
      </div>

      <!-- View All Button -->
      <div class="text-center mt-12">
        <BaseButton size="lg" variant="outline">
          <svg
            class="w-5 h-5 mr-2"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9.5a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z"
            />
          </svg>
          Barcha yangiliklarni ko'rish
        </BaseButton>
      </div>
    </div>
  </section>
</template>
