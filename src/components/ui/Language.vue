<script setup lang="ts">
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue'
import Icon from '../common/Icon.vue'
import { computed, defineProps, defineEmits } from 'vue'

const props = defineProps<{
  languages: Array<{ label: string; value: string }>
  modelValue?: string
  size?: 'sm' | 'md' | 'lg'
}>()

const emit = defineEmits(['update:modelValue'])

const selectedLang = computed(
  () => props.languages.find((l) => l.value === props.modelValue) || props.languages[0],
)

const sizeClasses = computed(() => {
  switch (props.size) {
    case 'sm':
      return 'px-3 py-1.5 text-sm'
    case 'lg':
      return 'px-6 py-3 text-base'
    default:
      return 'px-4 py-2 text-sm' // Match BaseButton
  }
})

function selectLang(lang: { label: string; value: string }) {
  emit('update:modelValue', lang.value)
}
</script>

<template>
  <Menu as="div" class="relative inline-block text-left">
    <div>
      <MenuButton
        class="btn-unified min-w-20 h-10 border border-[var(--primary)] bg-transparent text-[var(--primary)] hover:bg-[var(--primary)] hover:text-[var(--text-inverse)] flex gap-x-2 items-center justify-center transition-all duration-300 group"
        :class="sizeClasses"
      >
        <span class="font-semibold uppercase tracking-wide">{{ selectedLang.label }}</span>
        <Icon
          name="Globe"
          :size="16"
          class="text-current transition-transform duration-300 group-hover:scale-110"
        />
      </MenuButton>
    </div>

    <transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="transform scale-95 opacity-0"
      enter-to-class="transform scale-100 opacity-100"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="transform scale-100 opacity-100"
      leave-to-class="transform scale-95 opacity-0"
    >
      <MenuItems
        class="absolute right-0 mt-3 w-24 origin-top-right bg-[var(--bg-primary)] shadow-[var(--shadow-lg)] ring-1 ring-[var(--border)] focus:outline-none rounded-xl overflow-hidden border border-[var(--border)]"
      >
        <div class="py-1">
          <MenuItem v-for="lang in languages" :key="lang.value" v-slot="{ active }">
            <button
              :class="[
                active
                  ? 'bg-[var(--primary)] text-[var(--text-inverse)]'
                  : 'text-[var(--text-primary)] hover:bg-[var(--bg-secondary)]',
                'group flex w-full items-center justify-center px-3 py-3 text-sm font-semibold uppercase tracking-wide transition-all duration-200',
              ]"
              @click="selectLang(lang)"
            >
              {{ lang.label }}
            </button>
          </MenuItem>
        </div>
      </MenuItems>
    </transition>
  </Menu>
</template>
