<!-- eslint-disable unicorn/explicit-length-check -->
<script setup lang="ts">
import { NuxtLink } from '#components'
import type { BaseButtonProps } from '@unshared/vue'

const props = defineProps<{
  icon?: string
  iconAppend?: string
  iconPrepend?: string
  iconExpand?: boolean

  // --- Styling.
  link?: boolean
  light?: boolean
  filled?: boolean
  rounded?: boolean
  rainbow?: boolean
  outlined?: boolean
  size?: '2xl' | 'lg' | 'md' | 'sm' | 'xl'
  variant?: Variant
} & BaseButtonProps>()

// eslint-disable-next-line @typescript-eslint/no-unused-vars
const slots = defineSlots<{
  default: () => VNode
}>()

const classes = computed(() => {
  const {
    size = 'md',
    link = false,
    light = false,
    filled = false,
    rounded = false,
    rainbow = false,
    outlined = false,
    variant = 'light',
  } = props

  const classesBase = {
    'rounded': !rounded,
    'rounded-full': rounded,
    'gap-x-1 text-xs md:text-sm': size === 'sm',
    'gap-x-2 text-sm md:text-base': size === 'md',
    'gap-x-3 text-base md:text-lg': size === 'lg',
    'gap-x-4 text-lg md:text-xl': size === 'xl',
    'gap-x-5 text-xl md:text-2xl': size === '2xl',
    'px-2 py-1 md:px-3 md:py-1': !link && size === 'sm',
    'px-2 py-1 md:px-4 md:py-2': !link && size === 'md',
    'px-3 py-2 md:px-4 md:py-3': !link && size === 'lg',
    'px-3 py-2 md:px-5 md:py-3': !link && size === 'xl',
    'px-7 py-5 md:px-8 md:py-6': !link && size === '2xl',
    'opacity-90 hover:opacity-100': true,
  }

  const classesLink = {
    'hover:saturate-150': true,
    'text-primary-700': variant === 'primary',
    'text-secondary-700': variant === 'secondary',
    'text-success-700': variant === 'success',
    'text-danger-700': variant === 'danger',
    'text-warning-700': variant === 'warning',
    'text-accent-700': variant === 'accent',
    'text-black': variant === 'light',
  }

  const classesLinkDark = {
    'dark:text-primary-50': variant === 'primary',
    'dark:text-secondary-50': variant === 'secondary',
    'dark:text-success-50': variant === 'success',
    'dark:text-danger-50': variant === 'danger',
    'dark:text-warning-50': variant === 'warning',
    'dark:text-accent-50': variant === 'accent',
    'dark:text-light-50': variant === 'light',
  }

  const classesLight = {
    'ring-0 focus:ring-2 focus:ring-offset-2 hover:ring-offset-0 hover:ring-2': true,
    'ring-primary-600 text-primary-600 bg-primary-50': variant === 'primary',
    'ring-secondary-600 text-secondary-600 bg-secondary-50': variant === 'secondary',
    'ring-success-600 text-success-600 bg-success-50': variant === 'success',
    'ring-danger-600 text-danger-600 bg-danger-50': variant === 'danger',
    'ring-warning-600 text-warning-600 bg-warning-50': variant === 'warning',
    'ring-accent-600 text-accent-600 bg-accent-50': variant === 'accent',
    'text-black bg-light-50': variant === 'light',
  }

  const classesOutlined = {
    'ring-2 focus:ring-offset-2 hover:ring-offset-0 hover:ring-4 backdrop-blur-md': true,
    'ring-primary-600 text-primary-600': variant === 'primary',
    'ring-secondary-600 text-secondary-600': variant === 'secondary',
    'ring-success-600 text-success-600': variant === 'success',
    'ring-danger-600 text-danger-600': variant === 'danger',
    'ring-warning-600 text-warning-600': variant === 'warning',
    'ring-accent-600 text-accent-600': variant === 'accent',
    'ring-black text-black': variant === 'light',
  }

  const classesOutlineDark = {
    'dark:ring-primary-200 dark:text-primary-200': variant === 'primary',
    'dark:ring-secondary-200 dark:text-secondary-200': variant === 'secondary',
    'dark:ring-success-200 dark:text-success-200': variant === 'success',
    'dark:ring-danger-200 dark:text-danger-200': variant === 'danger',
    'dark:ring-warning-200 dark:text-warning-200': variant === 'warning',
    'dark:ring-accent-200 dark:text-accent-200': variant === 'accent',
    'dark:ring-light-200 dark:text-light-200': variant === 'light',
  }

  const classesFilled = {
    'ring-0 focus:ring-2 focus:ring-offset-2 hover:ring-offset-0 hover:ring-2': true,
    'text-white ring-primary-600 bg-primary-600': variant === 'primary',
    'text-white ring-secondary-600 bg-secondary-600': variant === 'secondary',
    'text-white ring-success-600 bg-success-600': variant === 'success',
    'text-white ring-danger-600 bg-danger-600': variant === 'danger',
    'text-white ring-warning-600 bg-warning-600': variant === 'warning',
    'text-white ring-accent-600 bg-accent-600': variant === 'accent',
    'text-black ring-light-600 bg-light-600': variant === 'light',
  }

  const classRainbow = {
    'bg-gradient-to-br from-secondary-500 via-primary-500 to-accent-600 text-white': true,
    'hover:saturate-150 hover:scale-105 bg-[size:200%] hover:bg-[size:100%]': true,
  }

  return {
    ...classesBase,
    ...link ? { ...classesLink, ...classesLinkDark } : {},
    ...light ? classesLight : {},
    ...filled ? classesFilled : {},
    ...outlined ? { ...classesOutlined, ...classesOutlineDark } : {},
    ...rainbow ? classRainbow : {},
  }
})

const iconClasses = computed(() => {
  const { size = 'md', iconExpand } = props
  return {

    'w-3 h-3': size === 'sm',
    'w-5 h-5': size === 'md',
    'w-6 h-6': size === 'lg',
    'w-7 h-7': size === 'xl',
    'transition-transform duration-100 ease-out': true,
    'group-hover:last:translate-x-1': iconExpand,
  }
})

const barClasses = computed(() => {
  const { variant = 'light' } = props
  return {
    'dark:bg-primary-100 bg-primary-600': variant === 'primary',
    'dark:bg-secondary-100 bg-secondary-600': variant === 'secondary',
    'dark:bg-success-100 bg-success-600': variant === 'success',
    'dark:bg-danger-100 bg-danger-600': variant === 'danger',
    'dark:bg-warning-100 bg-warning-600': variant === 'warning',
    'dark:bg-accent-100 bg-accent-600': variant === 'accent',
    'dark:bg-light-100 bg-black': variant === 'light',
  }
})
</script>

<template>
  <BaseButton
    class="
      inline-flex items-center justify-center font-bold focus:outline-none
      transition-all duration-100 ease-out relative group
    "
    :class="classes"
    v-bind="props"
    v-slot="slotProps"
    :as="to ? NuxtLink : undefined">

    <!-- Icon -->
    <BaseIcon
      as="i"
      v-if="iconPrepend || icon"
      :icon="iconPrepend || icon"
      :class="iconClasses"
      load
    />

    <!-- Content -->
    <slot v-bind="slotProps">
      <span v-if="label" v-text="label" />
    </slot>

    <!-- Bottom bar -->
    <div
      v-if="link"
      :class="barClasses"
      class="
        absolute -bottom-1 left-0 h-0.5 rounded-full
        translate-x-1/2
        w-1 opacity-0
        group-hover:w-full
        group-hover:opacity-100
        group-hover:translate-x-0
        transition-all duration-100 ease-out
      "
    />

    <!-- Icon -->
    <BaseIcon
      as="i"
      v-if="iconAppend || slotProps.isLoading"
      :icon="slotProps.isLoading ? 'i-line-md:loading-loop' : iconAppend"
      :class="iconClasses"
      load
    />
  </BaseButton>
</template>
