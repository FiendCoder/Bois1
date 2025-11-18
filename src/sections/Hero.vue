<script setup lang="ts">
const emit = defineEmits<{ (e: 'open-connect'): void }>()

import featherUrl from '@/assets/feather.png'
import benAvatarUrl from '@/assets/ben-avatar.png'
import womanHeroUrl from '@/assets/woman-hero.png'
</script>

<template>
  <section class="relative bg-white">

    <div class="relative md:hidden min-h-[520px]">
      <div class="absolute inset-0">
        <img
          :src="womanHeroUrl"
          alt="Model"
          class="w-full h-full object-cover object-[75%_0]"
        />
        <div class="absolute inset-0 bg-white/82" />
      </div>

      <div
        class="relative page-container pt-35 pb-16 flex items-center justify-center"
      >
        <div class="max-w-xs text-center">
          <h1
            class="text-3xl leading-[1.3]
                   tracking-[0.1em] text-[#4a637a]"
          >
            COLLAGEN IS<br />
            THE FOUNTAIN<br />
            OF YOUTH
          </h1>

          <p
            class="mt-4 text-sm tracking-[0.1em]
                   text-gray-500 uppercase"
          >
            WHAT’S YOUR INFLUENCE?
          </p>

          <div class="mt-8 flex justify-center">
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
        </div>
      </div>
    </div>

   
    <div
      class="hidden md:grid page-container px-20
             grid-cols-[1.3fr_1fr] items-center gap-10
             min-h-[540px]"
    >

      <div class="relative flex items-center">
    
        <img
          :src="featherUrl"
          alt=""
          class="pointer-events-none select-none
                 absolute left-[-40px] bottom-[-140px]
                 w-[520px] lg:w-[560px]"
        />

     
        <div class="relative z-10 max-w-xl">
          <h1
            class="text-[32px] lg:text-[40px] leading-[1.3]
                   tracking-[0.14em] text-[#4a637a]"
          >
            COLLAGEN IS<br />
            THE FOUNTAIN<br />
            OF YOUTH
          </h1>

          <p
            class="mt-4 text-sm lg:text-[15px] tracking-[0.1em]
                   text-gray-500 uppercase"
          >
            WHAT’S YOUR INFLUENCE?
          </p>

          <div class="mt-10">
            <button
              class="inline-flex items-center gap-3 rounded-full
                     bg-[#38566e] text-white px-8 py-3 shadow-lg
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
        </div>
      </div>

   
      <div class="flex items-stretch justify-end">
        <img
          :src="womanHeroUrl"
          alt="Model"
          class="h-[540px] w-auto object-cover object-[60%_0]"
        />
      </div>
    </div>
  </section>
</template>
