<script setup lang="ts">
type Influencer = {
  id: string
  name: string
  handle: string
  image: string
  avatar: string
}


import imgGrace from '@/assets/grace.png'
import imgBella from '@/assets/bella.png'
import imgGigi from '@/assets/gigi.png'

import avatarGrace from '@/assets/grace.png'
import avatarBella from '@/assets/bella.png'
import avatarGigi from '@/assets/gigi.png'

const influencers: Influencer[] = [
  {
    id: 'grace',
    name: 'Grace Perez',
    handle: '@graceperez',
    image: imgGrace,
    avatar: avatarGrace,
  },
  {
    id: 'bella',
    name: 'Bella Marie',
    handle: '@bellamarie',
    image: imgBella,
    avatar: avatarBella,
  },
  {
    id: 'gigi',
    name: 'Gigi Hadid',
    handle: '@gigihadid',
    image: imgGigi,
    avatar: avatarGigi,
  },
]
</script>

<template>
  <section class="bg-white">
    <div class=" page-container py-12 sm:py-16 lg:py-24">
      
      <div class="max-w-xl mx-auto text-center mb-10 lg:mb-14">
        <h2
          class="text-[18px] sm:text-[28px] tracking-[0.06em]
                 text-[#4a637a]  uppercase"
        >
          WHAT’S YOUR INFLUENCE?
        </h2>
        <p
          class="mt-4 text-[13px] sm:text-[14px] leading-relaxed
                 text-[#7b8a99]"
        >
          Is this you? Could this be you?
          Are you ready to be an influencer?
        </p>
      </div>

    
      <div
        class="grid grid-cols-1 md:grid-cols-3 gap-8 lg:gap-10"
      >
        <article
          v-for="person in influencers"
          :key="person.id"
          class="bg-white rounded-[26px] shadow-[0_18px_35px_rgba(0,0,0,0.12)]
                 overflow-hidden max-w-xs mx-auto md:mx-0"
        >
          
          <div class="w-full">
            <img
              :src="person.image"
              :alt="person.name"
              class="w-full h-auto object-cover"
            />
          </div>

         
          <div class="font-poppins px-6 py-4 flex items-center gap-3">
            <img
              :src="person.avatar"
              :alt="person.name"
              class="w-9 h-9 rounded-full object-cover"
            />
            <div class="leading-tight">
              <p class="text-[13px] font-semibold text-[#4a637a]">
                {{ person.name }}
              </p>
              <p class="text-[11px] text-[#9aa8b7]">
                {{ person.handle }}
              </p>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>
