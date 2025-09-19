<script setup lang="ts">
import { ref } from 'vue'
import BaseButton from '@/components/ui/BaseButton.vue'
import BaseInput from '@/components/ui/BaseInput.vue'
import BaseSelect from '@/components/ui/BaseSelect.vue'

const contactForm = ref({
  name: '',
  phone: '',
  email: '',
  subject: '',
  message: '',
})

const subjectOptions = [
  { label: 'Kurslar haqida', value: 'courses' },
  { label: "Ro'yxatdan o'tish", value: 'registration' },
  { label: 'Filiallar haqida', value: 'branches' },
  { label: "O'qituvchilar haqida", value: 'teachers' },
  { label: 'Boshqa savol', value: 'other' },
]

const contactInfo = [
  {
    icon: 'M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z',
    title: 'Telefon',
    details: ['+998 90 123 45 67', '+998 91 234 56 78'],
    description: 'Har kuni 8:00 dan 20:00 gacha',
  },
  {
    icon: 'M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75',
    title: 'Email',
    details: ['info@quran-course.uz', 'support@quran-course.uz'],
    description: '24 soat ichida javob beramiz',
  },
  {
    icon: 'M15 10.5a3 3 0 11-6 0 3 3 0 016 0z M19.5 10.5c0 7.142-7.5 11.25-7.5 11.25S4.5 17.642 4.5 10.5a7.5 7.5 0 1115 0z',
    title: 'Manzil',
    details: ['Toshkent sh., Chilonzor t., 5-mavze', 'Metro: Chilonzor'],
    description: "Asosiy o'quv markaz",
  },
  {
    icon: 'M12 6v6h4.5m4.5 0a9 9 0 11-18 0 9 9 0 0118 0z',
    title: 'Ish vaqti',
    details: ['Dushanba - Juma: 8:00-20:00', 'Shanba - Yakshanba: 9:00-18:00'],
    description: 'Bayramda dam olish kunlari',
  },
]

const socialLinks = [
  {
    name: 'Telegram',
    url: 'https://t.me/quran_course',
    icon: 'M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z M15 12a3 3 0 11-6 0 3 3 0 016 0z',
    color: 'from-blue-500 to-blue-600',
  },
  {
    name: 'Instagram',
    url: 'https://instagram.com/quran_course',
    icon: 'M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z M15 12a3 3 0 11-6 0 3 3 0 016 0z',
    color: 'from-pink-500 to-purple-600',
  },
  {
    name: 'YouTube',
    url: 'https://youtube.com/quran_course',
    icon: 'M5.25 5.653c0-.856.917-1.398 1.667-.986l11.54 6.348a1.125 1.125 0 010 1.971l-11.54 6.347a1.125 1.125 0 01-1.667-.985V5.653z',
    color: 'from-red-500 to-red-600',
  },
]

const submitForm = () => {
  // Form submission logic
  console.log('Contact form submitted:', contactForm.value)
  alert('Xabaringiz yuborildi! Tez orada aloqaga chiqamiz.')

  // Reset form
  contactForm.value = {
    name: '',
    phone: '',
    email: '',
    subject: '',
    message: '',
  }
}
</script>

<template>
  <section class="bg-gray-50 py-20">
    <div class="max-w-7xl mx-auto px-4">
      <!-- Header -->
      <div class="text-center mb-16">
        <h2 class="text-3xl font-bold text-gray-900 mb-4">Biz bilan bog'laning</h2>
        <p class="text-gray-600 max-w-2xl mx-auto">
          Savollaringiz bormi? Biz doimo sizga yordam berishga tayyormiz
        </p>
      </div>

      <div class="grid lg:grid-cols-2 gap-12">
        <!-- Contact Info -->
        <div class="space-y-6">
          <div
            v-for="info in contactInfo"
            :key="info.title"
            class="bg-white p-6 rounded-lg border border-gray-200"
          >
            <div class="flex items-center gap-4 mb-4">
              <div class="w-10 h-10 bg-gray-100 rounded-lg flex items-center justify-center">
                <svg
                  class="w-5 h-5 text-gray-600"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" :d="info.icon" />
                </svg>
              </div>
              <h3 class="font-semibold text-gray-900">{{ info.title }}</h3>
            </div>
            <div class="space-y-1 mb-3">
              <p v-for="detail in info.details" :key="detail" class="text-gray-700">
                {{ detail }}
              </p>
            </div>
            <p class="text-sm text-gray-500">{{ info.description }}</p>
          </div>

          <!-- Social Links -->
          <div class="bg-white p-6 rounded-lg border border-gray-200">
            <h3 class="font-semibold text-gray-900 mb-4">Ijtimoiy tarmoqlar</h3>
            <div class="flex gap-3">
              <a
                v-for="social in socialLinks"
                :key="social.name"
                :href="social.url"
                target="_blank"
                rel="noopener noreferrer"
                class="w-10 h-10 rounded-lg bg-gray-100 hover:bg-gray-200 flex items-center justify-center text-gray-600 hover:text-gray-700 transition-colors"
              >
                <svg
                  class="w-5 h-5"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  viewBox="0 0 24 24"
                >
                  <path stroke-linecap="round" stroke-linejoin="round" :d="social.icon" />
                </svg>
              </a>
            </div>
          </div>
        </div>

        <!-- Contact Form -->
        <div class="bg-white p-8 rounded-lg border border-gray-200">
          <h3 class="text-xl font-bold text-gray-900 mb-6">Xabar yuborish</h3>

          <form @submit.prevent="submitForm" class="space-y-6">
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <BaseInput
                label="Ism familiya"
                v-model="contactForm.name"
                placeholder="To'liq ismingizni kiriting"
                required
              />
              <BaseInput
                label="Telefon raqami"
                v-model="contactForm.phone"
                placeholder="+998 90 123 45 67"
                required
              />
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
              <BaseInput
                label="Email manzil"
                type="email"
                v-model="contactForm.email"
                placeholder="email@example.com"
              />
              <BaseSelect
                label="Mavzu"
                v-model="contactForm.subject"
                :options="subjectOptions"
                placeholder="Mavzuni tanlang"
                required
              />
            </div>

            <div>
              <label class="block mb-2 text-sm font-semibold text-gray-700">Xabar matni</label>
              <textarea
                v-model="contactForm.message"
                rows="4"
                placeholder="Xabaringizni bu yerga yozing..."
                class="w-full border border-gray-300 rounded-lg px-4 py-2.5 focus:outline-none focus:border-gray-900 focus:ring-2 focus:ring-gray-900/10 transition-all bg-white text-gray-900 placeholder-gray-500 resize-vertical"
                required
              ></textarea>
            </div>

            <BaseButton type="submit" size="lg" class="w-full">
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
                  d="M6 12L3.269 3.126A59.768 59.768 0 0121.485 12 59.77 59.77 0 013.27 20.876L5.999 12zm0 0h7.5"
                />
              </svg>
              Xabar yuborish
            </BaseButton>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
