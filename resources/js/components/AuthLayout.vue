<script setup>
import { computed } from 'vue';

const props = defineProps({
  imagePosition: {
    type: String,
    default: 'left', // 'left' atau 'right'
    validator: (value) => ['left', 'right'].includes(value)
  },
  imageSrc: {
    type: String,
    default: '/images/asrama/building.jpg'
  }
});

// Computed untuk order classes
const imageOrder = computed(() => {
  return props.imagePosition === 'left' 
    ? 'lg:order-first' 
    : 'lg:order-last';
});

const formOrder = computed(() => {
  return props.imagePosition === 'left' 
    ? 'lg:order-last' 
    : 'lg:order-first';
});
</script>

<template>
  <!-- Mobile: Image top, Form bottom -->
  <!-- Desktop: Configurable via props -->
  <div class="min-h-screen flex flex-col lg:flex-row bg-gray-50 dark:bg-gray-900">
    
    <!-- IMAGE SECTION -->
    <div 
      :class="[imageOrder, 'w-full lg:w-1/2 relative order-first']"
      class="h-64 lg:h-auto"
    >
      <!-- Background Image -->
      <img 
        :src="imageSrc" 
        alt="Asrama Putra Al-Basthomi"
        class="absolute inset-0 w-full h-full object-cover"
      />
      
      <!-- Overlay Gradient -->
      <div class="absolute inset-0 bg-gradient-to-br from-asrama-blue-600/90 to-asrama-blue-800/90"></div>
      
      <!-- Logo & Branding -->
      <div class="relative z-10 flex flex-col items-center justify-center h-full text-white px-8">
        <img 
          src="/images/asrama/logo.png" 
          alt="Logo Asrama" 
          class="w-24 h-24 mb-6"
          @error="$event.target.style.display='none'"
        />
        <h1 class="text-3xl lg:text-4xl font-bold text-center mb-2">
          Asrama Putra Al-Basthomi
        </h1>
        <p class="text-lg lg:text-xl text-blue-100 text-center">
          Mojosari
        </p>
      </div>
    </div>

    <!-- FORM SECTION -->
    <div 
      :class="[formOrder, 'w-full lg:w-1/2 flex items-center justify-center p-8 lg:p-12']"
      class="order-last"
    >
      <div class="w-full max-w-md">
        <slot /> <!-- Form content goes here -->
      </div>
    </div>

  </div>
</template>
