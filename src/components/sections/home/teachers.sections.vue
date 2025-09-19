<script setup lang="ts">
import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination, Autoplay } from "swiper/modules";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

const teachers = [
  {
    id: 1,
    name: "Ustoz Ahmad Karimov",
    speciality: "Qur'on Tilovati",
    experience: "15 yil tajriba",
    image: "/api/placeholder/300/300",
  },
  {
    id: 2,
    name: "Ustoza Fatima Abdullayeva",
    speciality: "Qur'on O'qish",
    experience: "12 yil tajriba",
    image: "/api/placeholder/300/300",
  },
  {
    id: 3,
    name: "Ustoz Bobur Toshmatov",
    speciality: "Tajvid",
    experience: "18 yil tajriba",
    image: "/api/placeholder/300/300",
  },
];

const modules = [Navigation, Pagination, Autoplay];
</script>

<template>
  <section class="py-24 bg-[var(--bg-secondary)]">
    <div class="max-w-7xl mx-auto px-6">
      <!-- Simple Header -->
      <div class="text-center mb-16">
        <div
          class="inline-flex items-center px-4 py-2 bg-[var(--accent)]/10 text-[var(--accent)] rounded-full text-sm font-medium mb-4"
        >
          Bizning Jamoa
        </div>
        <h2 class="text-4xl md:text-5xl font-bold text-gray-900 mb-6">
          O'qituvchilarimiz
        </h2>
        <p class="text-lg text-[var(--text-secondary)] max-w-3xl mx-auto">
          Malakali va tajribali ustozlarimiz bilan Qur'onni o'rganing
        </p>
      </div>

      <!-- Simple Teachers Carousel -->
      <div class="relative">
        <Swiper
          :modules="modules"
          :slides-per-view="1"
          :space-between="20"
          :autoplay="{
            delay: 3000,
            disableOnInteraction: false,
          }"
          :pagination="{ clickable: true }"
          :navigation="true"
          :loop="true"
          :breakpoints="{
            640: {
              slidesPerView: 2,
              spaceBetween: 20,
            },
            1024: {
              slidesPerView: 3,
              spaceBetween: 24,
            },
          }"
          class="teachers-swiper pb-16"
        >
          <SwiperSlide v-for="teacher in teachers" :key="teacher.id">
            <div
              class="bg-white p-6 rounded-xl border border-gray-200 shadow-sm text-center h-full flex flex-col"
            >
              <!-- Teacher Avatar -->
              <div class="w-20 h-20 mx-auto mb-4">
                <img
                  :src="
                    teacher.image ||
                    `https://ui-avatars.com/api/?name=${encodeURIComponent(teacher.name)}&background=random&color=fff&size=80&rounded=true`
                  "
                  :alt="teacher.name"
                  class="w-full h-full rounded-full object-cover shadow-md"
                  @error="
                    ($event.target as HTMLImageElement).src =
                      `https://ui-avatars.com/api/?name=${encodeURIComponent(teacher.name)}&background=random&color=fff&size=80&rounded=true`
                  "
                />
              </div>

              <!-- Teacher Info -->
              <div class="flex-grow">
                <h3 class="text-lg font-bold text-[var(--text-primary)] mb-2">
                  {{ teacher.name }}
                </h3>
                <p class="text-[var(--accent)] font-semibold mb-2">
                  {{ teacher.speciality }}
                </p>
                <p class="text-[var(--text-secondary)] text-sm">
                  {{ teacher.experience }}
                </p>
              </div>
            </div>
          </SwiperSlide>
        </Swiper>
      </div>
    </div>
  </section>
</template>

<style scoped>
.teachers-swiper {
  padding-bottom: 3rem;
}

:deep(.swiper-pagination) {
  bottom: 0;
}

:deep(.swiper-pagination-bullet) {
  background: #d1d5db;
  opacity: 1;
  width: 12px;
  height: 12px;
  margin: 0 6px;
}

:deep(.swiper-pagination-bullet-active) {
  background: var(--accent);
}

:deep(.swiper-button-next),
:deep(.swiper-button-prev) {
  color: var(--accent);
  top: 45%;
}

:deep(.swiper-button-next:after),
:deep(.swiper-button-prev:after) {
  font-size: 18px;
  font-weight: bold;
}
</style>
