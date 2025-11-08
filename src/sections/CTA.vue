<script setup lang="ts">
const emit = defineEmits<{ (e: 'open-connect'): void }>()

import benAvatarUrl from '@/assets/ben-avatar.png'
</script>

<template>
  <section class="bg-[#eef1f4]">
    <div
      class="page-container py-8 lg:py-10
             flex flex-col lg:flex-row items-center justify-between gap-6"
    >
      
      <h2
        class="text-[16px] lg:text-[18px] tracking-[0.22em]
               text-[#4a637a] font-semibold uppercase
               text-center lg:text-left leading-tight"
      >
        WOULD YOU LIKE TO<br class="hidden sm:block" />
        LEARN MORE?
      </h2>

      
      <button
        class="inline-flex items-center gap-3 rounded-full
               bg-[#38566e] text-white px-6 py-3 shadow-lg
               hover:brightness-110 transition"
        @click="emit('open-connect')"
      >
        <img
          :src="benAvatarUrl"
          alt="Ben"
          class="w-8 h-8 rounded-full border-2 border-white object-cover"
        />
        <span class="text-sm font-semibold tracking-wide">
          Connect with Ben
        </span>
      </button>
    </div>
  </section>
</template>
