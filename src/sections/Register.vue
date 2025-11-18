<script setup lang="ts">
import ConnectForm from '../components/ConnectForm.vue'


import registerSideImg from '@/assets/register.png'
import registerBgImg from '@/assets/register-bg.png'
</script>

<template>
  <section class="relative">
    
    <div class="absolute inset-0">
      <img
        :src="registerBgImg"
        alt="Background"
        class="w-full h-full object-cover"
      />
      <div class="absolute inset-0 bg-black/70" />
    </div>

   
    <div class="relative page-container py-8 lg:py-10 flex justify-center">
      <div
        class="w-full max-w-2xl bg-white shadow-2xl overflow-hidden
               grid md:grid-cols-[0.7fr_1fr]"
      >
    
        <div class="relative hidden md:block">
          <img
            :src="registerSideImg"
            alt="Smiling man using phone"
            class="w-full h-full object-cover"
          />
        </div>

       
        <div class="px-5 py-5 sm:px-6 sm:py-6">
          <h3
            class="text-[15px] sm:text-[16px] tracking-[0.2em]
                   text-[#4a637a]  uppercase mb-6"
          >
            REGISTER TO LEARN MORE
          </h3>

          <ConnectForm />
        </div>
      </div>
    </div>
  </section>
</template>
