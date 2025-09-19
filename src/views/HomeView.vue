<script setup lang="ts">
import HeroSections from "@/components/sections/home/hero.sections.vue";
import WhyChoiseUs from "@/components/sections/home/why-choise-us.vue";
import HowWeWork from "@/components/sections/home/how-we-work.vue";
import TeachersSections from "@/components/sections/home/teachers.sections.vue";
import StudentsSections from "@/components/sections/home/students.sections.vue";
import MapSection from "@/components/sections/home/map-section.vue";
</script>

<template>
  <div class="flex flex-col">
    <HeroSections />
    <WhyChoiseUs />
    <HowWeWork />
    <TeachersSections />
    <StudentsSections />
    <MapSection />
  </div>
</template>
