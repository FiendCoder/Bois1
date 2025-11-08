<script setup lang="ts">
import { Dialog, DialogPanel, TransitionRoot } from '@headlessui/vue'
import ConnectNowForm from './ConnectNowForm.vue'

const props = defineProps<{ open: boolean }>()

const emit = defineEmits<{
  (e: 'close'): void
}>()

function handleSubmitted(values: any) {
  console.log('connect modal submitted:', values)
  emit('close')
}
</script>

<template>
  <TransitionRoot :show="props.open">
    <Dialog class="relative z-50" @close="emit('close')">
      
      <div class="fixed inset-0 bg-black/40" aria-hidden="true" />


      <div class="fixed inset-0 flex items-center justify-center px-4">
        <DialogPanel
          class="w-full max-w-md bg-white rounded-2xl shadow-2xl px-6 py-6 sm:px-8 sm:py-8"
        >
          <div class="flex items-start justify-between mb-6">
            <h3
              class="text-[16px] sm:text-[18px] tracking-[0.22em]
                     text-[#4a637a] font-semibold uppercase"
            >
              CONNECT WITH BEN
            </h3>
            <button
              type="button"
              class="text-gray-400 hover:text-gray-600"
              @click="emit('close')"
            >
              ✕
            </button>
          </div>

        
          <ConnectNowForm @submitted="handleSubmitted" />
        </DialogPanel>
      </div>
    </Dialog>
  </TransitionRoot>
</template>
