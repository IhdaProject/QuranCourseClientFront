<template>
  <div class="space-y-2">
    <!-- Label -->
    <label v-if="props.label" class="block text-sm font-medium text-[var(--text-primary)]">
      {{ props.label }}
      <span v-if="props.error" class="text-[var(--error)] ml-1">*</span>
    </label>

    <!-- Select Container -->
    <div class="relative">
      <select
        :value="props.modelValue"
        :disabled="props.disabled"
        :multiple="props.multiple"
        :class="[
          sizeClasses,
          selectClasses,
          {
            'opacity-50 cursor-not-allowed': props.disabled,
          },
        ]"
        @change="handleChange"
      >
        <option
          v-if="props.placeholder && !props.multiple"
          value=""
          disabled
          selected
          class="text-[var(--text-muted)]"
        >
          {{ props.placeholder }}
        </option>
        <option
          v-for="option in props.options"
          :key="option.value"
          :value="option.value"
          :disabled="option.disabled"
          class="text-[var(--text-primary)] bg-[var(--bg-primary)]"
        >
          {{ option.label }}
        </option>
      </select>

      <!-- Dropdown Icon -->
      <div class="absolute right-3 top-1/2 transform -translate-y-1/2 pointer-events-none">
        <svg
          v-if="!props.error && !props.success"
          class="w-5 h-5 text-[var(--text-muted)]"
          fill="none"
          stroke="currentColor"
          stroke-width="1.5"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M8.25 15L12 18.75 15.75 15m-7.5-6L12 5.25 15.75 9"
          />
        </svg>

        <!-- Error Icon -->
        <svg
          v-if="props.error"
          class="w-5 h-5 text-[var(--error)]"
          fill="none"
          stroke="currentColor"
          stroke-width="1.5"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M12 9v3.75m9-.75a9 9 0 11-18 0 9 9 0 0118 0zm-9 3.75h.008v.008H12v-.008z"
          />
        </svg>

        <!-- Success Icon -->
        <svg
          v-if="props.success"
          class="w-5 h-5 text-[var(--success)]"
          fill="none"
          stroke="currentColor"
          stroke-width="1.5"
          viewBox="0 0 24 24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
          />
        </svg>
      </div>
    </div>

    <!-- Helper Text -->
    <div v-if="props.error || props.success || props.hint" class="text-xs">
      <p v-if="props.error" class="text-[var(--error)] font-medium">{{ props.error }}</p>
      <p v-else-if="props.success" class="text-[var(--success)] font-medium">{{ props.success }}</p>
      <p v-else-if="props.hint" class="text-[var(--text-muted)]">{{ props.hint }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Option {
  label: string
  value: string | number
  disabled?: boolean
}

interface Props {
  modelValue: string | number | null
  label?: string
  placeholder?: string
  options: Option[]
  error?: string
  success?: string
  hint?: string
  disabled?: boolean
  size?: 'sm' | 'md' | 'lg'
  multiple?: boolean
}

const props = withDefaults(defineProps<Props>(), {
  disabled: false,
  size: 'md',
  multiple: false,
})

const emit = defineEmits<{
  'update:modelValue': [value: string | number | string[] | number[]]
  change: [value: string | number | string[] | number[]]
}>()

const sizeClasses = computed(() => {
  switch (props.size) {
    case 'sm':
      return 'px-3 py-2 text-sm'
    case 'lg':
      return 'px-4 py-3 text-lg'
    default:
      return 'px-4 py-2.5 text-base'
  }
})

const selectClasses = computed(() => {
  const base = 'input-modern w-full appearance-none bg-[var(--bg-primary)] pr-10'

  if (props.error) {
    return `${base} border-[var(--error)] focus:border-[var(--error)] focus:ring-[var(--error)]/10`
  }

  if (props.success) {
    return `${base} border-[var(--success)] focus:border-[var(--success)] focus:ring-[var(--success)]/10`
  }

  return `${base} border-[var(--border-primary)] focus:border-[var(--border-focus)]`
})

const handleChange = (event: Event) => {
  const target = event.target as HTMLSelectElement
  const value = props.multiple
    ? Array.from(target.selectedOptions).map((option) => option.value)
    : target.value

  emit('update:modelValue', value)
  emit('change', value)
}
</script>
