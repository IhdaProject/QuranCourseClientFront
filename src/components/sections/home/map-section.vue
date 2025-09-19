<script setup lang="ts">
import { ref } from "vue";
import UzbekistanMapSVG from "../../common/UzbekistanMapSVG.vue";
import ChangeRegionModal from "@/components/common/ChangeRegionModal.vue";
import BaseButton from "@/components/ui/BaseButton.vue";
import BaseFileUpload from "@/components/ui/BaseFileUpload.vue";
import BaseInput from "@/components/ui/BaseInput.vue";
import BaseSelect from "@/components/ui/BaseSelect.vue";

interface Course {
  address: string;
  phone: string;
  students: number;
  waiting: number;
}

interface Region {
  id: number;
  name: string;
  course: Course;
}

const regions: Region[] = [
  {
    id: 1,
    name: "Toshkent shahri",
    course: {
      address: "Toshkent shahri, Chilonzor tumani, 5-mavze",
      phone: "+998 90 123 45 67",
      students: 150,
      waiting: 30,
    },
  },
  {
    id: 2,
    name: "Andijon viloyati",
    course: {
      address: "Andijon shahri, Boburshox ko'chasi, 12-uy",
      phone: "+998 90 234 56 78",
      students: 120,
      waiting: 25,
    },
  },
  {
    id: 3,
    name: "Buxoro viloyati",
    course: {
      address: "Buxoro shahri, Ibn Sino ko'chasi, 8-uy",
      phone: "+998 90 345 67 89",
      students: 100,
      waiting: 20,
    },
  },
  {
    id: 4,
    name: "Jizzax viloyati",
    course: {
      address: "Jizzax shahri, Amir Temur ko'chasi, 15-uy",
      phone: "+998 90 456 78 90",
      students: 90,
      waiting: 15,
    },
  },
  {
    id: 5,
    name: "Qashqadaryo viloyati",
    course: {
      address: "Qarshi shahri, Alisher Navoiy ko'chasi, 10-uy",
      phone: "+998 90 567 89 01",
      students: 110,
      waiting: 22,
    },
  },
  {
    id: 6,
    name: "Navoiy viloyati",
    course: {
      address: "Navoiy shahri, Al-Xorazmiy ko'chasi, 7-uy",
      phone: "+998 90 678 90 12",
      students: 95,
      waiting: 18,
    },
  },
  {
    id: 7,
    name: "Namangan viloyati",
    course: {
      address: "Namangan shahri, Boburshox ko'chasi, 13-uy",
      phone: "+998 90 789 01 23",
      students: 105,
      waiting: 20,
    },
  },
  {
    id: 8,
    name: "Samarqand viloyati",
    course: {
      address: "Samarqand shahri, Registon ko'chasi, 11-uy",
      phone: "+998 90 890 12 34",
      students: 130,
      waiting: 28,
    },
  },
  {
    id: 9,
    name: "Surxandaryo viloyati",
    course: {
      address: "Termiz shahri, Ibn Sino ko'chasi, 9-uy",
      phone: "+998 90 901 23 45",
      students: 85,
      waiting: 15,
    },
  },
  {
    id: 10,
    name: "Sirdaryo viloyati",
    course: {
      address: "Guliston shahri, Amir Temur ko'chasi, 14-uy",
      phone: "+998 90 012 34 56",
      students: 80,
      waiting: 12,
    },
  },
  {
    id: 11,
    name: "Toshkent viloyati",
    course: {
      address: "Nurafshon shahri, Alisher Navoiy ko'chasi, 16-uy",
      phone: "+998 90 123 45 67",
      students: 140,
      waiting: 32,
    },
  },
  {
    id: 12,
    name: "Farg'ona viloyati",
    course: {
      address: "Farg'ona shahri, Boburshox ko'chasi, 17-uy",
      phone: "+998 90 234 56 78",
      students: 125,
      waiting: 28,
    },
  },
  {
    id: 13,
    name: "Xorazm viloyati",
    course: {
      address: "Urganch shahri, Al-Xorazmiy ko'chasi, 18-uy",
      phone: "+998 90 345 67 89",
      students: 95,
      waiting: 18,
    },
  },
  {
    id: 14,
    name: "Qoraqalpog'iston Respublikasi",
    course: {
      address: "Nukus shahri, Amir Temur ko'chasi, 19-uy",
      phone: "+998 90 456 78 90",
      students: 90,
      waiting: 15,
    },
  },
];

const selectedRegion = ref<Region | null>(null);
const openModal = ref<boolean>(false);

const form = ref({
  lastName: "",
  passport: "",
  fatherName: "",
  jshshir: "",
  phone: "",
  gender: "",
  passportFile: null as File | null,
  photo: null as File | null,
});

const formErrors = ref({
  lastName: "",
  passport: "",
  phone: "",
});

const genderOptions = [
  { label: "Erkak", value: "male" },
  { label: "Ayol", value: "female" },
];

const selectRegion = (id: number) => {
  selectedRegion.value = regions.find((region) => region.id === id) || null;
  openModal.value = true;
};

const submitForm = () => {
  // Clear previous errors
  formErrors.value = { lastName: "", passport: "", phone: "" };

  // Form validation
  let hasErrors = false;

  if (!form.value.lastName.trim()) {
    formErrors.value.lastName = "Familiya majburiy";
    hasErrors = true;
  }

  if (!form.value.passport.trim()) {
    formErrors.value.passport = "Pasport raqami majburiy";
    hasErrors = true;
  }

  if (!form.value.phone.trim()) {
    formErrors.value.phone = "Telefon raqami majburiy";
    hasErrors = true;
  }

  if (hasErrors) {
    return;
  }

  // Form submission logic here
  console.log("Form submitted:", form.value);
  console.log("Selected region:", selectedRegion.value?.name);

  // Success message and close modal
  alert(
    `Muvaffaqiyatli ro'yxatdan o'tdingiz! ${selectedRegion.value?.name} filialimizda o'qishingiz mumkin.`
  );
  openModal.value = false;

  // Reset form
  form.value = {
    lastName: "",
    passport: "",
    fatherName: "",
    jshshir: "",
    phone: "",
    gender: "",
    passportFile: null,
    photo: null,
  };
};
</script>

<template>
  <section id="map-section" class="bg-white py-16 lg:py-24">
    <div class="container mx-auto px-4">
      <div class="text-center mb-16">
        <h2 class="heading-lg text-brand mb-4">
          O'zbekiston bo'ylab filiallarimiz
        </h2>
        <p class="body-lg text-gray-600 max-w-2xl mx-auto">
          Barcha viloyatlardagi kurslarimiz haqida ma'lumot oling va yaqin
          filialga yoziling
        </p>
      </div>
      <div class="mt-10">
        <div
          class="bg-gradient-to-br from-slate-50 to-blue-50 p-8 rounded-2xl shadow-lg border border-slate-200"
        >
          <h3 class="heading-sm text-brand mb-6 text-center">
            O'zbekiston Xaritasi
            <span class="text-gray-500">(Viloyatni tanlang)</span>
          </h3>
          <UzbekistanMapSVG
            :selectedRegion="selectedRegion?.id"
            @update:selectedRegion="selectRegion"
          />
        </div>
      </div>
    </div>
    <!-- Change region modal -->
    <change-region-modal v-model="openModal">
      <template #title>
        {{ selectedRegion?.name }}
      </template>
      <template #body>
        <div class="flex flex-col lg:flex-row gap-6">
          <!-- Region info -->
          <div
            class="flex-1 bg-gradient-to-br from-gray-50 to-blue-50 rounded-xl p-6 border border-gray-200 shadow-sm"
          >
            <div class="flex items-start justify-between mb-4">
              <div>
                <h2 class="text-lg font-bold text-gray-900 mb-1">
                  {{ selectedRegion?.name }}
                </h2>
                <div
                  class="inline-flex items-center px-2 py-1 rounded-full text-xs font-medium bg-gray-700 text-white"
                >
                  Qur'on kursi
                </div>
              </div>
              <div class="text-right">
                <div class="text-xs text-gray-500">Jami talabalar</div>
                <div class="text-xl font-bold text-green-600">
                  {{ selectedRegion?.course.students }}
                </div>
              </div>
            </div>

            <div class="space-y-4">
              <div class="flex items-start gap-3">
                <div
                  class="w-8 h-8 bg-gradient-to-br from-gray-600 to-blue-600 rounded-lg flex items-center justify-center flex-shrink-0"
                >
                  <svg
                    class="w-4 h-4 text-white"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"
                    />
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"
                    />
                  </svg>
                </div>
                <div>
                  <div class="text-sm font-semibold text-gray-800 mb-1">
                    Manzil
                  </div>
                  <div class="text-sm text-gray-600">
                    {{ selectedRegion?.course.address }}
                  </div>
                </div>
              </div>

              <div class="flex items-start gap-3">
                <div
                  class="w-8 h-8 bg-gradient-to-br from-green-500 to-green-600 rounded-lg flex items-center justify-center flex-shrink-0"
                >
                  <svg
                    class="w-4 h-4 text-white"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"
                    />
                  </svg>
                </div>
                <div>
                  <div class="text-sm font-semibold text-gray-800 mb-1">
                    Telefon
                  </div>
                  <a
                    :href="`tel:${selectedRegion?.course.phone}`"
                    class="text-sm text-blue-600 hover:text-blue-700 font-medium transition-colors duration-200"
                  >
                    {{ selectedRegion?.course.phone }}
                  </a>
                </div>
              </div>

              <div
                class="flex items-center justify-between p-3 bg-gradient-to-r from-amber-50 to-orange-50 rounded-lg border border-amber-200"
              >
                <div>
                  <div class="text-xs font-semibold text-amber-800">
                    Navbatdagi talabalar
                  </div>
                  <div class="text-lg font-bold text-amber-900">
                    {{ selectedRegion?.course.waiting }} kishi
                  </div>
                </div>
                <div
                  class="w-8 h-8 bg-gradient-to-br from-amber-400 to-orange-500 rounded-full flex items-center justify-center"
                >
                  <svg
                    class="w-4 h-4 text-white"
                    fill="none"
                    stroke="currentColor"
                    stroke-width="2"
                    viewBox="0 0 24 24"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"
                    />
                  </svg>
                </div>
              </div>
            </div>
          </div>

          <!-- Form -->
          <div class="flex-1">
            <div
              class="bg-white rounded-xl p-6 border border-gray-200 shadow-lg"
            >
              <h3 class="text-lg font-bold text-gray-900 mb-4">
                Ro'yxatdan o'ting
              </h3>

              <form class="space-y-4">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <BaseInput
                    label="Familiya"
                    v-model="form.lastName"
                    placeholder="Familiyangizni kiriting"
                    :error="formErrors.lastName"
                  />

                  <BaseInput
                    label="Otasining ismi"
                    v-model="form.fatherName"
                    placeholder="Otasining ismini kiriting"
                  />
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <BaseInput
                    label="Pasport seriya raqami"
                    v-model="form.passport"
                    placeholder="AA1234567"
                    :error="formErrors.passport"
                  />

                  <BaseInput
                    label="JSHSHIR"
                    v-model="form.jshshir"
                    placeholder="12345678901234"
                  />
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <BaseInput
                    label="Telefon raqami"
                    v-model="form.phone"
                    placeholder="+998 99 123 45 67"
                    :error="formErrors.phone"
                  />

                  <BaseSelect
                    label="Jinsi"
                    v-model="form.gender"
                    :options="genderOptions"
                    placeholder="Jinsni tanlang"
                  />
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                  <BaseFileUpload
                    label="Pasport nusxasi"
                    v-model="form.passportFile"
                    accept="image/*,.pdf"
                    file-type-text="JPG, PNG yoki PDF (max 5MB)"
                  />

                  <BaseFileUpload
                    label="3x4 rasm"
                    v-model="form.photo"
                    accept="image/*"
                    file-type-text="JPG yoki PNG (max 2MB)"
                  />
                </div>
              </form>
            </div>
          </div>
        </div>
      </template>
      <template #footer>
        <div
          class="flex flex-col sm:flex-row gap-3 justify-end px-4 py-3 rounded-b-xl !w-full"
        >
          <BaseButton
            @click="openModal = false"
            variant="outline"
            class="flex-1 sm:flex-initial"
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
                d="M6 18L18 6M6 6l12 12"
              />
            </svg>
            Bekor qilish
          </BaseButton>
          <BaseButton
            @click="submitForm"
            type="button"
            class="flex-1 sm:flex-initial"
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
                d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"
              />
            </svg>
            Ro'yxatdan o'tish
          </BaseButton>
        </div>
      </template>
    </change-region-modal>
  </section>
</template>
