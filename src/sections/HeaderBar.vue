<script setup lang="ts">
import { ref } from 'vue'

 
import iconLinkedIn from '@/assets/icon-linkedin.png'
import iconFacebook from '@/assets/icon-facebook.png'
import iconSlack from '@/assets/icon-slack.png'
import iconTwitter from '@/assets/icon-twitter.png'
import iconMenu from '@/assets/dropdown.png'

type NavItem = {
  label: string
  target: string
}

const navItems: NavItem[] = [
  { label: 'HOME',            target: 'hero' },
  { label: 'SHOP',            target: 'products' },
  { label: 'ABOUT US',        target: 'about' },
  { label: 'BE AN INFLUENCER', target: 'influencers' },
]

const mobileOpen = ref(false)

function scrollToSection(id: string) {
  if (id === 'hero') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  } else {
    const el = document.getElementById(id)
    if (el) {
      el.scrollIntoView({ behavior: 'smooth', block: 'start' })
    }
  }
  mobileOpen.value = false
}

function toggleMobile() {
  mobileOpen.value = !mobileOpen.value
}
</script>

<template>
  <header
    class="fixed top-0 left-0 right-0 z-40 bg-white/95 backdrop-blur "
  >
    
    <div class="page-container py-4 flex items-center justify-between gap-4">
     
      <div class="flex items-center gap-4">
        
        <button
          type="button"
          class="md:hidden w-8 h-8 grid place-items-center text-[#4a637a]"
          @click="toggleMobile"
        >
          <img
    :src="iconMenu"
    alt="Open navigation"
    class="w-5 h-5 object-contain"
  />
        </button>

      
        <div class="text-2xl sm:text-3xl font-bold tracking-[0.25em] text-black">
          LOGO
        </div>
      </div>

      
      <div class="flex items-center gap-6">
        
        <nav class="hidden md:flex items-center gap-8 text-xs tracking-[0.2em]">
          <button
            v-for="item in navItems"
            :key="item.label"
            class="uppercase"
            :class="[
              item.label === 'HOME'
                ? 'text-[#38566e]'
                : 'text-[#a2b0bc] hover:text-[#38566e]'
            ]"
            @click="scrollToSection(item.target)"
          >
            {{ item.label }}
          </button>
        </nav>

         
        <div class="flex items-center gap-3">
            <button
            type="button"
            class="w-12 h-12 grid place-items-center"
          >
            <img :src="iconFacebook" alt="Facebook" class="w-4 h-4 object-contain" />
          </button>
          <button
            type="button"
            class="w-12 h-12 grid place-items-center"
          >
            <img :src="iconLinkedIn" alt="LinkedIn" class="w-4 h-4 object-contain" />
          </button>
          
          <button
            type="button"
            class="w-12 h-12  grid place-items-center"
          >
            <img :src="iconSlack" alt="Slack" class="w-4 h-4 object-contain" />
          </button>
          <button
            type="button"
            class="w-12 h-12  grid place-items-center"
          >
            <img :src="iconTwitter" alt="Twitter" class="w-4 h-4 object-contain" />
          </button>
        </div>
      </div>
    </div>

     
    <div
      v-if="mobileOpen"
      class="md:hidden border-t border-gray-100 bg-white/95"
    >
      <div
        class="page-container py-3 flex flex-col gap-2 text-xs tracking-[0.28em]"
      >
        <button
          v-for="item in navItems"
          :key="item.label"
          class="uppercase text-left py-1 text-[#4a637a]"
          @click="scrollToSection(item.target)"
        >
          {{ item.label }}
        </button>
      </div>
    </div>
  </header>
</template>
