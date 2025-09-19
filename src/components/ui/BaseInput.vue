<template>
  <div class="space-y-2">
    <!-- Label -->
    <label v-if="props.label" class="block text-sm font-medium text-[var(--text-primary)]">
      {{ props.label }}
      <span v-if="props.error" class="text-[var(--error)] ml-1">*</span>
    </label>

    <!-- Input Container -->
    <div class="relative">
      <!-- Left Icon -->
      <div
        v-if="props.icon && props.iconPosition === 'left'"
        class="absolute left-3 top-1/2 transform -translate-y-1/2 text-[var(--text-secondary)] pointer-events-none"
      >
        <svg
          class="w-5 h-5"
          fill="none"
          stroke="currentColor"
          stroke-width="1.5"
          viewBox="0 0 24 24"
        >
          <!-- Add icon paths here based on icon prop -->
        </svg>
      </div>

      <!-- Input Field -->
      <input
        :type="props.type"
        :placeholder="props.placeholder"
        :value="props.modelValue"
        :disabled="props.disabled"
        :readonly="props.readonly"
        :class="[
          sizeClasses,
          variantClasses,
          {
            'pl-10': props.icon && props.iconPosition === 'left',
            'pr-10': props.icon && props.iconPosition === 'right',
            'opacity-50 cursor-not-allowed': props.disabled,
            'bg-[var(--bg-secondary)] cursor-default': props.readonly,
          },
        ]"
        @input="handleInput"
        @focus="emit('focus', $event as FocusEvent)"
        @blur="emit('blur', $event as FocusEvent)"
      />

      <!-- Right Icon -->
      <div
        v-if="props.icon && props.iconPosition === 'right'"
        class="absolute right-3 top-1/2 transform -translate-y-1/2 text-[var(--text-secondary)] pointer-events-none"
      >
        <svg
          class="w-5 h-5"
          fill="none"
          stroke="currentColor"
          stroke-width="1.5"
          viewBox="0 0 24 24"
        >
          <!-- Add icon paths here based on icon prop -->
        </svg>
      </div>

      <!-- Status Icon -->
      <div
        v-if="props.error || props.success"
        class="absolute right-3 top-1/2 transform -translate-y-1/2 pointer-events-none"
      >
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
      <p v-else-if="props.hint" class="text-[var(--text-secondary)]">{{ props.hint }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
  modelValue: string | number | null
  label?: string
  placeholder?: string
  type?: 'text' | 'email' | 'password' | 'number' | 'tel' | 'url'
  error?: string
  success?: string
  hint?: string
  disabled?: boolean
  readonly?: boolean
  size?: 'sm' | 'md' | 'lg'
  variant?: 'default' | 'filled' | 'underlined'
  icon?: string
  iconPosition?: 'left' | 'right'
}

const props = withDefaults(defineProps<Props>(), {
  type: 'text',
  disabled: false,
  readonly: false,
  size: 'md',
  variant: 'default',
  iconPosition: 'left',
})

const emit = defineEmits<{
  'update:modelValue': [value: string | number]
  focus: [event: FocusEvent]
  blur: [event: FocusEvent]
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

const variantClasses = computed(() => {
  const base = 'input-modern w-full'

  if (props.error) {
    return `${base} border-[var(--error)] focus:border-[var(--error)] focus:ring-[var(--error)]/10`
  }

  if (props.success) {
    return `${base} border-[var(--success)] focus:border-[var(--success)] focus:ring-[var(--success)]/10`
  }

  switch (props.variant) {
    case 'filled':
      return `${base} bg-[var(--bg-secondary)] border-transparent focus:bg-[var(--bg-primary)]`
    case 'underlined':
      return `${base} bg-transparent border-0 border-b-2 border-[var(--border)] rounded-none focus:border-[var(--border-focus)]`
    default:
      return `${base} border-[var(--border)] focus:border-[var(--border-focus)]`
  }
})

const handleInput = (event: Event) => {
  const target = event.target as HTMLInputElement
  emit('update:modelValue', target.value)
}
</script>
