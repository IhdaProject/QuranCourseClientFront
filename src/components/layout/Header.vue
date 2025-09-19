<script setup lang="ts">
import { ref } from "vue";
import Language from "../ui/Language.vue";
import BaseButton from "../ui/BaseButton.vue";

const menuItems = [
  { label: "Bosh sahifa", href: "#home" },
  { label: "Biz haqimizda", href: "#about" },
  { label: "Ustozlar", href: "#teachers" },
  { label: "Aloqa", href: "#contact" },
];

const languages = [
  { value: "uz", label: "UZB" },
  { value: "cyrl", label: "CYRL" },
];

const selectedLang = ref("uz");
const langOpen = ref(false);
const mobileMenuOpen = ref(false);

const selectLang = (value: string) => {
  selectedLang.value = value;
  langOpen.value = false;
};

const toggleMobileMenu = () => {
  mobileMenuOpen.value = !mobileMenuOpen.value;
};

const scrollToMap = () => {
  const mapSection = document.querySelector("#map-section");
  if (mapSection) {
    mapSection.scrollIntoView({ behavior: "smooth" });
  }
};
</script>

<template>
  <header
    class="bg-[var(--bg-primary)] border-b border-[var(--border)] sticky top-0 left-0 w-full z-50 shadow-[var(--shadow)] backdrop-blur-sm bg-opacity-95"
  >
    <div class="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
      <!-- Logo -->
      <div class="flex items-center gap-3 group cursor-pointer">
        <div
          class="w-12 h-12 bg-gradient-to-br from-[var(--primary)] to-[var(--accent)] rounded-xl flex items-center justify-center shadow-lg group-hover:shadow-xl transition-all duration-300 group-hover:scale-105"
        >
          <svg
            class="w-7 h-7 text-white"
            fill="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"
              stroke="currentColor"
              stroke-width="1.5"
              fill="none"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </div>
        <div>
          <h1
            class="text-xl font-bold text-[var(--text-primary)] group-hover:text-[var(--primary)] transition-colors"
          >
            Qur'on
          </h1>
          <p class="text-sm text-[var(--text-secondary)] font-medium">
            Kurslari
          </p>
        </div>
      </div>

      <!-- Desktop Navigation -->
      <nav class="hidden md:flex items-center gap-1">
        <a
          v-for="item in menuItems"
          :key="item.href"
          :href="item.href"
          class="px-4 py-2 text-[var(--text-secondary)] hover:text-[var(--primary)] hover:bg-[var(--bg-secondary)] rounded-lg transition-all duration-300 font-medium relative group"
        >
          {{ item.label }}
        </a>
      </nav>

      <!-- Right Actions -->
      <div class="flex items-center gap-4">
        <!-- Language Selector -->
        <Language
          :languages="languages"
          v-model="selectedLang"
          @select="selectLang"
        />

        <!-- CTA Button - Desktop -->
        <div class="hidden md:block">
          <BaseButton variant="primary" size="md" @click="scrollToMap">
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
                d="M9 5H7a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"
              />
            </svg>
            Navbatni Tekshirish
          </BaseButton>
        </div>

        <!-- Mobile Menu Toggle -->
        <button
          class="md:hidden p-2 text-[var(--text-secondary)] hover:text-[var(--primary)] hover:bg-[var(--bg-secondary)] rounded-lg transition-all duration-300"
          @click="toggleMobileMenu"
        >
          <svg
            class="w-6 h-6"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            viewBox="0 0 24 24"
          >
            <path
              v-if="!mobileMenuOpen"
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M4 6h16M4 12h16M4 18h16"
            />
            <path
              v-else
              stroke-linecap="round"
              stroke-linejoin="round"
              d="M6 18L18 6M6 6l12 12"
            />
          </svg>
        </button>
      </div>
    </div>

    <!-- Mobile Navigation Menu -->
    <transition
      enter-active-class="transition-all duration-300 ease-out"
      enter-from-class="opacity-0 -translate-y-2"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition-all duration-200 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-2"
    >
      <div
        v-if="mobileMenuOpen"
        class="md:hidden bg-[var(--bg-primary)] border-t border-[var(--border)] px-4 py-6 shadow-[var(--shadow-lg)]"
      >
        <nav class="space-y-4">
          <a
            v-for="item in menuItems"
            :key="item.href"
            :href="item.href"
            class="block py-3 px-4 text-[var(--text-secondary)] hover:text-[var(--primary)] hover:bg-[var(--bg-secondary)] rounded-lg transition-all duration-300 font-medium"
            @click="mobileMenuOpen = false"
          >
            {{ item.label }}
          </a>
        </nav>

        <!-- Mobile CTA Button -->
        <div class="mt-6 pt-4 border-t border-[var(--border)]">
          <BaseButton
            variant="primary"
            size="md"
            :full-width="true"
            @click="scrollToMap"
          >
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
                d="M9 5H7a2 2 0 00-2 2v10a2 2 0 002 2h8a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"
              />
            </svg>
            Navbatni Tekshirish
          </BaseButton>
        </div>
      </div>
    </transition>
  </header>
</template>
