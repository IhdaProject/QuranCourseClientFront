<script setup lang="ts">
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination, Autoplay } from "swiper/modules";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";
import Icon from "@/components/common/Icon.vue";

const testimonials = [
  {
    id: 1,
    name: "Aziza Karimova",
    age: "24 yosh",
    course: "Qur'on O'qish",
    message:
      "Professional ustozlar bilan Qur'onni to'g'ri o'qishni o'rgandim. Juda samarali offline ta'lim.",
    rating: 5,
    duration: "6 oy",
    // achievement: 'Tajvid asoslari',
  },
  {
    id: 2,
    name: "Muhammad Ali",
    age: "19 yosh",
    course: "Qur'on O'qish",
    message:
      "Eng yaxshi joy. Ustozlar har doim yordam berishga tayyor. Juda yaxshi muhit.",
    rating: 5,
    duration: "2 yil",
    // achievement: '10 para yod',
  },
  {
    id: 3,
    name: "Maryam Toshmatova",
    age: "32 yosh",
    course: "Qur'on O'qish",
    message:
      "Qur'onni tushunib o'qish imkoniyati paydo bo'ldi. Har bir oyat ma'nosini o'rganish juda foydali.",
    rating: 5,
    duration: "1 yil",
    // achievement: 'Arabcha asoslari',
  },
  {
    id: 4,
    name: "Otabek Rahmonov",
    age: "28 yosh",
    course: "Qur'on O'qish",
    message:
      "Ustozlarning professional yondashuvi va individual e'tibor juda yoqdi. Har bir darsdan foyda oldim.",
    rating: 5,
    duration: "8 oy",
  },
  {
    id: 5,
    name: "Nilufar Karimova",
    age: "21 yosh",
    course: "Qur'on O'qish",
    message:
      "Qisqa muddat ichida Qur'onni to'g'ri o'qishni o'rgandim. Juda qulay va samarali ta'lim tizimi.",
    rating: 5,
    duration: "4 oy",
  },
];

const stats = [
  {
    number: "1500+",
    label: "Faol talabalar",
  },
  {
    number: "300+",
    label: "Bitiruvchilar",
  },
  {
    number: "98%",
    label: "Muvaffaqiyat ko'rsatkichi",
  },
  {
    number: "5★",
    label: "O'rtacha baho",
  },
];

const modules = [Navigation, Pagination, Autoplay];
</script>

<template>
  <section class="section-unified bg-[var(--bg-primary)]">
    <div class="container-unified">
      <!-- Header -->
      <div class="text-center mb-16">
        <div
          class="inline-flex items-center px-4 py-2 bg-[var(--accent)]/10 text-[var(--accent)] rounded-full text-sm font-medium mb-4"
        >
          Talabalar Fikrlari
        </div>
        <h2 class="section-title">Bizning Talabalarimiz</h2>
        <p class="section-subtitle">
          O'quvchilarimizning muvaffaqiyatlari va Qur'on o'rganishdagi
          tajribalari
        </p>
      </div>

      <!-- Stats Grid -->
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 mb-16">
        <div
          v-for="stat in stats"
          :key="stat.label"
          class="card-unified text-center hover:border-[var(--accent)]/30"
        >
          <div class="text-3xl md:text-4xl font-bold text-[var(--accent)] mb-3">
            {{ stat.number }}
          </div>
          <div class="text-sm text-[var(--text-secondary)] font-medium">
            {{ stat.label }}
          </div>
        </div>
      </div>

      <!-- Testimonials -->
      <div class="relative">
        <Swiper
          :modules="modules"
          :slides-per-view="1"
          :space-between="24"
          :autoplay="{
            delay: 4000,
            disableOnInteraction: false,
          }"
          :pagination="{ clickable: true }"
          :navigation="true"
          :breakpoints="{
            640: {
              slidesPerView: 2,
              spaceBetween: 24,
            },
            1024: {
              slidesPerView: 3,
              spaceBetween: 24,
            },
          }"
          class="testimonials-swiper pb-16"
        >
          <SwiperSlide
            v-for="testimonial in testimonials"
            :key="testimonial.id"
          >
            <div class="card-unified h-full hover:border-[var(--accent)]/30">
              <!-- Header -->
              <div class="flex items-start justify-between mb-6">
                <div>
                  <h3
                    class="text-xl font-semibold text-[var(--text-primary)] mb-2"
                  >
                    {{ testimonial.name }}
                  </h3>
                  <div
                    class="flex items-center gap-2 text-sm text-[var(--text-secondary)] mb-2"
                  >
                    <Icon name="Clock" :size="16" />
                    <span class="font-medium">{{ testimonial.duration }}</span>
                    <span>•</span>
                    <span>{{ testimonial.age }}</span>
                  </div>
                </div>
                <div class="flex items-center gap-1">
                  <Icon name="Star" :size="18" class="text-[var(--accent)]" />
                  <span class="text-lg font-bold text-[var(--text-primary)]">{{
                    testimonial.rating
                  }}</span>
                </div>
              </div>

              <!-- Course Badge -->
              <div class="mb-6">
                <span
                  class="inline-block px-4 py-2 bg-[var(--accent)]/10 text-[var(--accent)] text-sm rounded-full font-medium"
                >
                  {{ testimonial.course }}
                </span>
              </div>

              <!-- Message -->
              <p class="text-[var(--text-secondary)] leading-relaxed italic">
                "{{ testimonial.message }}"
              </p>
            </div>
          </SwiperSlide>
        </Swiper>
      </div>
    </div>
  </section>
</template>

<style scoped>
.testimonials-swiper {
  padding-bottom: 3rem;
}

:deep(.swiper-pagination) {
  bottom: 0;
}

:deep(.swiper-pagination-bullet) {
  background: #d15db;
  opacity: 1;
  width: 12px;
  height: 12px;
  margin: 0 6px;
}

:deep(.swiper-pagination-bullet-active) {
  background: #f59e0b;
}

:deep(.swiper-button-next),
:deep(.swiper-button-prev) {
  color: #f59e0b;
  background: white;
  border-radius: 50%;
  width: 48px;
  height: 48px;
  border: 2px solid #f59e0b;
  transition: all 0.3s ease;
}

:deep(.swiper-button-next:hover),
:deep(.swiper-button-prev:hover) {
  background: #f59e0b;
  color: white;
  box-shadow: 0 8px 20px rgba(16, 185, 129, 0.3);
  transform: scale(1.1);
}

:deep(.swiper-button-next):after,
:deep(.swiper-button-prev):after {
  font-size: 18px;
  font-weight: bold;
}
</style>
