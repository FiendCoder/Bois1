<script setup lang="ts">
import { ref } from 'vue'

import HeaderBar from './sections/HeaderBar.vue'
import Hero from './sections/Hero.vue'
import Congratulations from './sections/Congratulations.vue'
import ProductGrid from './sections/ProductGrid.vue'
import InfluencerGrid from './sections/InfluencerGrid.vue'
import CTASection from './sections/CTA.vue'
import RegisterInline from './sections/Register.vue'
import SiteFooter from './sections/Footer.vue'
import ConnectModal from './components/ConnectModal.vue'

const showModal = ref(false)

const open = () => {
  showModal.value = true
}

const close = () => {
  showModal.value = false
}
</script>

<template>
  <div class="min-h-screen bg-white text-[#233241]">
    <!-- Header / navigation -->
    <HeaderBar />

    <main class="pt-24">
      <!-- HERO / BANNER -->
      <section id="hero">
        <Hero @open-connect="open" />
      </section>

      <!-- CONGRATULATIONS / ABOUT COPY -->
      <section id="congrats">
        <Congratulations />
      </section>

      <!-- PRODUCT GRID (SHOP) -->
      <section id="products">
        <ProductGrid />
      </section>

      <!-- INFLUENCER GRID -->
      <section id="influencers">
        <InfluencerGrid />
      </section>

      <!-- CTA STRIP (“Would you like to learn more?”) -->
      <section id="about">
        <CTASection @open-connect="open" />
      </section>

      <!-- INLINE REGISTER CARD -->
      <section id="register">
        <RegisterInline />
      </section>
    </main>

    <!-- FOOTER -->
    <SiteFooter />

    <!-- CONNECT WITH BEN MODAL -->
    <ConnectModal :open="showModal" @close="close" />
  </div>
</template>
