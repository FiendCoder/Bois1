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
  


  <section class="bg-[#f6f7f8]" id="products">
  
    <div class="page-container  md:px-40 py-12 sm:py-16 lg:py-24 space-y-14">
      <div
        v-for="p in products"
        :key="p.id"
        :class="[
          
          'flex flex-col gap-10 lg:gap-16 items-center md:justify-between',
          p.reverse ? 'md:flex-row-reverse' : 'md:flex-row'
        ]"
      >
    
        <div class="max-w-xl space-y-4">
          <h3
            class="text-[16px] lg:text-[28px] tracking-[0.1em] text-[#4a637a]
                    uppercase"
          >
            {{ p.title }}
          </h3>

          <p
            v-if="p.subtitle"
            class="text-sm  text-gray-500"
          >
            {{ p.subtitle }}
          </p>

          <div
            class="mt-2 border-l-[3px] border-[#d3dde5] pl-4
                   text-[13px] lg:text-[14px] leading-relaxed
                   text-[#7b8a99] space-y-1"
          >
            <p v-for="(line, i) in p.copy" :key="i">
              {{ line }}
            </p>
          </div>
        </div>

        <div class="flex-shrink-0">
          <div class="w-full max-w-[260px] lg:max-w-[280px]">
         
            <div
              v-if="!p.image"
              class="aspect-[4/3] rounded-xl bg-white shadow-md grid place-items-center text-xs text-gray-400"
            >
              Product image
            </div>
            <img
              v-else
              :src="p.image"
              :alt="p.title"
              class="w-full h-auto rounded-xl shadow-md object-cover"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
