<script setup lang="ts">
import Icon from "@/components/common/Icon.vue";

const currentYear = new Date().getFullYear();

const socialLinks = [
  { name: "Telegram", icon: "MessageCircle", href: "#", color: "bg-blue-500" },
  { name: "Instagram", icon: "Instagram", href: "#", color: "bg-pink-500" },
  { name: "YouTube", icon: "Youtube", href: "#", color: "bg-red-500" },
];

const quickLinks = [
  { label: "Biz haqimizda", href: "#about" },
  { label: "Kurslar", href: "#courses" },
  { label: "O'qituvchilar", href: "#teachers" },
  { label: "Filiallar", href: "#map-section" },
  { label: "Aloqa", href: "#contact" },
];

const courseLinks = [
  { label: "Qur'on tilovati", href: "#" },
  { label: "Tajvid asoslari", href: "#" },
  { label: "Arabcha darslari", href: "#" },
  { label: "Hafizlik kursi", href: "#" },
];

const contactInfo = [
  {
    icon: "Phone",
    value: "+998 90 123 45 67",
    description: "24/7 qo'ng'iroq markazi",
    href: "tel:+998901234567",
  },
  {
    icon: "Mail",
    value: "info@quran-kurs.uz",
    description: "Savollar uchun",
    href: "mailto:info@quran-kurs.uz",
  },
  {
    icon: "MapPin",
    value: "Toshkent, Chilonzor tumani",
    description: "Asosiy ofis manzili",
    href: "#map-section",
  },
];
</script>

<template>
  <footer
    class="bg-gradient-to-br from-slate-900 via-gray-900 to-slate-800 text-white relative overflow-hidden"
  >
    <!-- Background Pattern -->
    <div class="absolute inset-0 opacity-5">
      <div class="absolute top-0 left-0 w-full h-full">
        <svg
          width="100"
          height="100"
          viewBox="0 0 100 100"
          class="fill-current text-white"
        >
          <pattern
            id="grid"
            width="10"
            height="10"
            patternUnits="userSpaceOnUse"
          >
            <path
              d="M 10 0 L 0 0 0 10"
              fill="none"
              stroke="currentColor"
              stroke-width="0.5"
            />
          </pattern>
          <rect width="100" height="100" fill="url(#grid)" />
        </svg>
      </div>
    </div>

    <div class="relative max-w-7xl mx-auto px-6 py-20">
      <div
        class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 lg:gap-12"
      >
        <!-- Brand Section -->

        <!-- Quick Links -->
        <div>
          <h4 class="text-lg font-bold text-white mb-6 flex items-center">
            <span
              class="w-1 h-6 bg-gradient-to-b from-[var(--accent)] to-blue-500 rounded-full mr-3"
            ></span>
            Sahifalar
          </h4>
          <ul class="space-y-3">
            <li v-for="link in quickLinks" :key="link.label">
              <a
                :href="link.href"
                class="text-gray-300 hover:text-[var(--accent)] transition-all duration-300 flex items-center group py-1"
              >
                <span
                  class="w-0 group-hover:w-4 h-px bg-[var(--accent)] transition-all duration-300 mr-0 group-hover:mr-2"
                ></span>
                {{ link.label }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Course Links -->
        <div>
          <h4 class="text-lg font-bold text-white mb-6 flex items-center">
            <span
              class="w-1 h-6 bg-gradient-to-b from-[var(--accent)] to-blue-500 rounded-full mr-3"
            ></span>
            Kurslar
          </h4>
          <ul class="space-y-3">
            <li v-for="course in courseLinks" :key="course.label">
              <a
                :href="course.href"
                class="text-gray-300 hover:text-[var(--accent)] transition-all duration-300 flex items-center group py-1"
              >
                <span
                  class="w-0 group-hover:w-4 h-px bg-[var(--accent)] transition-all duration-300 mr-0 group-hover:mr-2"
                ></span>
                {{ course.label }}
              </a>
            </li>
          </ul>
        </div>

        <!-- Contact Section -->
        <div>
          <h4 class="text-lg font-bold text-white mb-6 flex items-center">
            <span
              class="w-1 h-6 bg-gradient-to-b from-[var(--accent)] to-blue-500 rounded-full mr-3"
            ></span>
            Aloqa
          </h4>
          <div class="space-y-4 mb-6">
            <a
              v-for="contact in contactInfo"
              :key="contact.value"
              :href="contact.href"
              class="flex items-start gap-3 group hover:bg-white/5 p-3 rounded-xl transition-all duration-300 border border-transparent hover:border-white/10"
            >
              <div
                class="w-10 h-10 bg-gradient-to-br from-[var(--accent)]/20 to-blue-500/20 rounded-xl flex items-center justify-center flex-shrink-0 group-hover:from-[var(--accent)] group-hover:to-blue-500 transition-all duration-300"
              >
                <Icon
                  :name="contact.icon"
                  :size="18"
                  class="text-[var(--accent)] group-hover:text-white transition-colors duration-300"
                />
              </div>
              <div>
                <div
                  class="text-white group-hover:text-[var(--accent)] transition-colors duration-300 font-medium"
                >
                  {{ contact.value }}
                </div>
                <div class="text-gray-400 text-sm mt-1">
                  {{ contact.description }}
                </div>
              </div>
            </a>
          </div>
        </div>
      </div>
    </div>

    <!-- Bottom Section -->
    <div class="relative border-t border-white/10 bg-black/20">
      <div class="max-w-7xl mx-auto px-6 py-6">
        <div
          class="flex flex-col lg:flex-row items-center justify-between gap-4"
        >
          <div class="flex flex-col sm:flex-row items-center gap-4">
            <p class="text-gray-400 text-sm text-center sm:text-left">
              © {{ currentYear }} Qur'on Kurslari. Barcha huquqlar
              himoyalangan.
            </p>
            <div class="flex items-center gap-4 text-sm">
              <a
                href="#"
                class="text-gray-400 hover:text-[var(--accent)] transition-colors duration-300"
                >Maxfiylik siyosati</a
              >
              <span class="text-gray-600">•</span>
              <a
                href="#"
                class="text-gray-400 hover:text-[var(--accent)] transition-colors duration-300"
                >Foydalanish shartlari</a
              >
            </div>
          </div>

          <div class="flex items-center gap-4">
            <div
              class="flex items-center gap-2 px-3 py-2 bg-green-500/10 border border-green-500/20 rounded-full"
            >
              <div
                class="w-2 h-2 bg-green-400 rounded-full animate-pulse"
              ></div>
              <span class="text-green-400 text-sm font-medium">Onlayn</span>
            </div>
            <div class="text-gray-400 text-sm hidden sm:block">
              O'zbekiston bo'ylab 15+ filial
            </div>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>
