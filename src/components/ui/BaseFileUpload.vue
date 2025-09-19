<template>
  <div class="space-y-2">
    <!-- Label -->
    <label v-if="props.label" class="block text-sm font-medium text-[var(--text-primary)]">
      {{ props.label }}
      <span v-if="props.error" class="text-[var(--error)] ml-1">*</span>
    </label>

    <!-- File Input Container -->
    <div class="relative">
      <!-- Hidden Input -->
      <input
        ref="fileInput"
        type="file"
        class="hidden"
        :accept="props.accept"
        :multiple="props.multiple"
        :disabled="props.disabled"
        @change="onFileChange"
      />

      <!-- Upload Area -->
      <div
        :class="[
          containerClasses,
          borderClasses,
          { 'opacity-50 cursor-not-allowed': props.disabled },
        ]"
        @click="!props.disabled && handleFileSelect()"
        @dragover="!props.disabled && handleDragOver"
        @dragleave="!props.disabled && handleDragLeave"
        @drop="!props.disabled && handleDrop"
      >
        <div class="flex flex-col items-center space-y-4">
          <!-- Icon -->
          <div class="relative">
            <div
              :class="[
                'w-12 h-12 flex items-center justify-center rounded-full transition-all duration-300',
                fileName
                  ? 'bg-[var(--success)] text-white'
                  : isDragging
                    ? 'bg-[var(--primary-accent)] text-white'
                    : 'bg-[var(--bg-secondary)] text-[var(--text-muted)] group-hover:bg-[var(--primary-accent)] group-hover:text-white',
              ]"
            >
              <!-- Success Icon -->
              <svg
                v-if="fileName && props.success"
                class="w-6 h-6"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
              </svg>

              <!-- Upload Icon -->
              <svg
                v-else
                class="w-6 h-6"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                viewBox="0 0 24 24"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"
                />
              </svg>
            </div>
          </div>

          <!-- Text Content -->
          <div class="text-center space-y-2">
            <div v-if="fileName" class="space-y-1">
              <p class="text-sm font-medium text-[var(--text-primary)] truncate max-w-xs">
                {{ fileName }}
              </p>
              <p v-if="fileSize" class="text-xs text-[var(--text-muted)]">
                {{ fileSize }}
              </p>
            </div>

            <div v-else class="space-y-1">
              <p class="text-sm text-[var(--text-primary)]">
                <span
                  class="font-semibold text-[var(--primary-accent)] hover:text-[var(--primary-dark)]"
                >
                  Fayl tanlash
                </span>
                <span class="text-[var(--text-muted)] ml-1">yoki bu yerga torting</span>
              </p>
              <p v-if="props.fileTypeText" class="text-xs text-[var(--text-muted)]">
                {{ props.fileTypeText }}
              </p>
            </div>
          </div>
        </div>

        <!-- Remove Button -->
        <button
          v-if="fileName && !props.disabled"
          @click.stop="removeFile"
          type="button"
          class="absolute top-2 right-2 w-8 h-8 bg-[var(--error)] hover:bg-red-700 text-white rounded-full flex items-center justify-center transition-colors duration-200 shadow-sm"
        >
          <svg
            class="w-4 h-4"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            viewBox="0 0 24 24"
          >
            <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
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
import { ref, watch, computed } from 'vue'

interface Props {
  modelValue: File | null
  label?: string
  accept?: string
  fileTypeText?: string
  error?: string
  success?: string
  hint?: string
  disabled?: boolean
  multiple?: boolean
  maxSize?: number // in MB
  variant?: 'default' | 'compact' | 'modern'
}

const props = withDefaults(defineProps<Props>(), {
  disabled: false,
  multiple: false,
  maxSize: 5,
  variant: 'default',
})

const emit = defineEmits<{
  'update:modelValue': [value: File | File[] | null]
  change: [value: File | File[] | null]
  error: [message: string]
}>()

const fileInput = ref<HTMLInputElement | null>(null)
const isDragging = ref(false)
const fileName = ref('')
const fileSize = ref('')

const containerClasses = computed(() => {
  const base = 'relative transition-all duration-300 cursor-pointer'

  if (props.variant === 'compact') {
    return `${base} border border-dashed rounded-lg p-4 text-center hover:border-[var(--primary-accent)] hover:bg-[var(--bg-secondary)]`
  }

  if (props.variant === 'modern') {
    return `${base} border-2 border-dashed rounded-xl p-8 text-center group`
  }

  return `${base} border-2 border-dashed rounded-xl p-6 text-center`
})

const borderClasses = computed(() => {
  if (props.error) {
    return 'border-[var(--error)] bg-[var(--error-light)]'
  }

  if (props.success || fileName.value) {
    return 'border-[var(--success)] bg-[var(--success-light)]'
  }

  if (isDragging.value) {
    return 'border-[var(--primary-accent)] bg-[var(--bg-secondary)]'
  }

  return 'border-[var(--border-primary)] hover:border-[var(--primary-accent)] hover:bg-[var(--bg-secondary)]'
})

const formatFileSize = (bytes: number): string => {
  if (bytes === 0) return '0 Bytes'
  const k = 1024
  const sizes = ['Bytes', 'KB', 'MB', 'GB']
  const i = Math.floor(Math.log(bytes) / Math.log(k))
  return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i]
}

const validateFile = (file: File): boolean => {
  if (file.size > props.maxSize * 1024 * 1024) {
    emit('error', `Fayl hajmi ${props.maxSize}MB dan oshmasligi kerak`)
    return false
  }
  return true
}

const handleFileSelect = () => {
  fileInput.value?.click()
}

const onFileChange = (event: Event) => {
  const files = (event.target as HTMLInputElement).files
  if (files && files.length > 0) {
    const file = files[0]

    if (validateFile(file)) {
      emit('update:modelValue', props.multiple ? Array.from(files) : file)
      emit('change', props.multiple ? Array.from(files) : file)
      fileName.value = file.name
      fileSize.value = formatFileSize(file.size)
    }
  } else {
    emit('update:modelValue', null)
    emit('change', null)
    fileName.value = ''
    fileSize.value = ''
  }
}

const removeFile = () => {
  emit('update:modelValue', null)
  emit('change', null)
  fileName.value = ''
  fileSize.value = ''
  if (fileInput.value) {
    fileInput.value.value = ''
  }
}

const handleDragOver = (event: DragEvent) => {
  event.preventDefault()
  isDragging.value = true
}

const handleDragLeave = () => {
  isDragging.value = false
}

const handleDrop = (event: DragEvent) => {
  event.preventDefault()
  isDragging.value = false

  const files = event.dataTransfer?.files
  if (files && files.length > 0) {
    const file = files[0]

    if (validateFile(file)) {
      emit('update:modelValue', props.multiple ? Array.from(files) : file)
      emit('change', props.multiple ? Array.from(files) : file)
      fileName.value = file.name
      fileSize.value = formatFileSize(file.size)
    }
  }
}

watch(
  () => props.modelValue,
  (val) => {
    if (val) {
      const file = Array.isArray(val) ? val[0] : val
      fileName.value = file.name
      fileSize.value = formatFileSize(file.size)
    } else {
      fileName.value = ''
      fileSize.value = ''
    }
  },
  { immediate: true },
)
</script>
