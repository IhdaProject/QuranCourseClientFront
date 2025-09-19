<script setup lang="ts">
import { defineProps, defineEmits, computed } from "vue";

interface Props {
  type?: "button" | "submit" | "reset";
  size?: "sm" | "md" | "lg";
  variant?: "primary" | "secondary" | "outline";
  disabled?: boolean;
  loading?: boolean;
  fullWidth?: boolean;
  loadingText?: string;
}

const props = withDefaults(defineProps<Props>(), {
  type: "button",
  size: "md",
  variant: "primary",
  disabled: false,
  loading: false,
  fullWidth: false,
  loadingText: "Yuklanmoqda...",
});

const emit = defineEmits<{
  click: [event: MouseEvent];
}>();

const sizeClasses = computed(() => {
  switch (props.size) {
    case "sm":
      return "px-3 py-1.5 text-sm";
    case "lg":
      return "px-6 py-3 text-base";
    default:
      return "px-4 py-2 text-sm"; // Made default smaller
  }
});

const variantClasses = computed(() => {
  const variants = {
    primary:
      "bg-[var(--primary)] hover:bg-[var(--primary-hover)] text-[var(--text-inverse)] border-transparent",
    secondary:
      "bg-[var(--bg-secondary)] hover:bg-gray-200 text-[var(--text-primary)] border-[var(--border)]",
    outline:
      "bg-transparent hover:bg-[var(--bg-secondary)] text-[var(--primary)] !border  !border-[var(--primary)]   !hover:border-[var(--primary-hover)]",
  };
  return variants[props.variant];
});

const handleClick = (event: MouseEvent) => {
  if (!props.disabled && !props.loading) {
    emit("click", event);
  }
};
</script>

<template>
  <button
    :type="props.type"
    :disabled="props.disabled || props.loading"
    :class="[
      ' btn-unified focus:outline-none focus:ring-2 focus:ring-[var(--primary)]/20 focus:ring-offset-1 disabled:opacity-50 disabled:cursor-not-allowed',
      sizeClasses,
      variantClasses,
      {
        'w-full': props.fullWidth,
        'pointer-events-none': props.loading,
      },
    ]"
    @click="handleClick"
  >
    <!-- Loading State -->
    <template v-if="props.loading">
      <svg
        class="animate-spin h-4 w-4"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
      >
        <circle
          class="opacity-25"
          cx="12"
          cy="12"
          r="10"
          stroke="currentColor"
          stroke-width="4"
        ></circle>
        <path
          class="opacity-75"
          fill="currentColor"
          d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
        ></path>
      </svg>
      <span>{{ props.loadingText }}</span>
    </template>

    <!-- Button Content -->
    <template v-else>
      <slot />
    </template>
  </button>
</template>
