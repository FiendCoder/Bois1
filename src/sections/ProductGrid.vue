<script setup lang="ts">
type Product = {
  id: string
  title: string
  subtitle?: string
  copy: string[]
  reverse?: boolean  
  image: string
}

 
import gelImg from '@/assets/gel.png'
import elixirImg from '@/assets/elixir.png'
import oilImg from '@/assets/oil.png'

const products: Product[] = [
  {
    id: 'gel',
    title: 'COLLAGEN PEPTIDE EXFOLIATING GEL',
    copy: [
      'Instant results with visible remove of dead cells.',
      'Clinically proven to activate the skin repair process.',
      'Smooths wrinkles, improves tone & elasticity.',
    ],
    reverse: false,
    image: gelImg,
  },
  {
    id: 'elixir',
    title: 'BELLA COLLAGEN ELIXIR',
    subtitle: 'Beauty from the Inside Out',
    copy: [
      'Helps the body product more collagen.',
      'Backed by double blind clinical studies.',
      'Healthier skin, hair, nails, joints & more.',
    ],
    reverse: true,
    image: elixirImg,
  },
  {
    id: 'oil',
    title: 'HYDRATING LIP PLUMPING OIL',
    copy: [
      'Ultimate softness, hydration, & comfort.',
      'A smooth and naturally-plump look.',
      'Shine of a gloss with the benefits of a balm.',
    ],
    reverse: false,
    image: oilImg,
  },
]
</script>

<template>
  <section class="bg-[#f6f7f8]">
    <div class="page-container py-12 sm:py-16 lg:py-24 space-y-14">
      <div
        v-for="p in products"
        :key="p.id"
        class="grid md:grid-cols-2 gap-8 lg:gap-12 items-center"
      >
       
        
        <div
          :class="[
            'flex justify-center mx-auto md:justify-end',
            p.reverse ? 'md:order-1 md:justify-start' : 'md:order-2 md:justify-end',
          ]"
        >
          <div class="w-full max-w-xs sm:max-w-sm">
            <img
              :src="p.image"
              :alt="p.title"
              class="w-full h-auto rounded-xl shadow-md object-cover"
            />
          </div>
        </div>

   
        <div
  :class="[
    
    'space-y-4 max-w-xs sm:max-w-sm mx-auto md:mx-0',
 
    p.reverse ? 'md:order-2 md:text-left' : 'md:order-1 md:text-left',
  ]"
>
          <h3
            class="text-[15px] sm:text-[16px] lg:text-[18px]
                   tracking-[0.18em] text-[#4a637a]
                   font-semibold uppercase"
          >
            {{ p.title }}
          </h3>

          <p
            v-if="p.subtitle"
            class="text-xs tracking-[0.2em] text-gray-500 uppercase"
          >
            {{ p.subtitle }}
          </p>

          <div
            class="mt-2 border-l-[3px] border-[#d3dde5] pl-4
                   text-[13px] lg:text-[14px]
                   leading-relaxed text-[#7b8a99] space-y-1"
          >
            <p v-for="(line, i) in p.copy" :key="i">
              {{ line }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
