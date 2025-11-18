<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { useForm, useField } from 'vee-validate'
import * as yup from 'yup'

const RECAPTCHA_SITE_KEY = '6LdTTBAsAAAAADUmBpbxdUPUlxVlc6garM3_68kk' 

const emit = defineEmits<{
  (e: 'submitted', payload: any): void
}>()


const schema = yup.object({
  firstName: yup.string().required('First name is required'),
  lastName: yup.string().required('Last name is required'),
  phone: yup.string().required('Phone is required'),
  email: yup.string().email('Enter a valid email').required('Email is required'),
})

const { handleSubmit, errors } = useForm({
  validationSchema: schema,
})

const { value: firstName } = useField<string>('firstName')
const { value: lastName } = useField<string>('lastName')
const { value: phone } = useField<string>('phone')
const { value: email } = useField<string>('email')


const recaptchaRef = ref<HTMLDivElement | null>(null)
const recaptchaToken = ref<string | null>(null)
const recaptchaError = ref<string | null>(null)

onMounted(() => {
  const interval = setInterval(() => {
    const w = window as any
    if (w.grecaptcha && recaptchaRef.value) {
      clearInterval(interval)
      w.grecaptcha.render(recaptchaRef.value, {
        sitekey: RECAPTCHA_SITE_KEY,
        callback: (token: string) => {
          recaptchaToken.value = token
          recaptchaError.value = null
        },
        'expired-callback': () => {
          recaptchaToken.value = null
        },
      })
    }
  }, 300)
})

const onSubmit = handleSubmit(values => {
 
  if (!recaptchaToken.value) {
    recaptchaError.value = 'Please confirm you are not a robot.'
    return
  }


  emit('submitted', {
    ...values,
    recaptchaToken: recaptchaToken.value,
  })
})
</script>

<template>
  <form @submit.prevent="onSubmit" class="space-y-4 max-w-sm">
    <div>
      <label class="block text-xs font-medium text-gray-500 mb-1">
        First Name
      </label>
      <input
        v-model="firstName"
        type="text"
        class="block w-full border-b border-[#d4dde5] focus:border-[#4a637a]
               outline-none py-1.5 text-sm"
      />
      <p v-if="errors.firstName" class="mt-0.5 text-xs text-red-500">
        {{ errors.firstName }}
      </p>
    </div>

    <div>
      <label class="block text-xs font-medium text-gray-500 mb-1">
        Last Name
      </label>
      <input
        v-model="lastName"
        type="text"
        class="block w-full border-b border-[#d4dde5] focus:border-[#4a637a]
               outline-none py-1.5 text-sm"
      />
      <p v-if="errors.lastName" class="mt-0.5 text-xs text-red-500">
        {{ errors.lastName }}
      </p>
    </div>

    <div>
      <label class="block text-xs font-medium text-gray-500 mb-1">
        Best Phone Number
      </label>
      <input
        v-model="phone"
        type="tel"
        class="block w-full border-b border-[#d4dde5] focus:border-[#4a637a]
               outline-none py-1.5 text-sm"
      />
      <p v-if="errors.phone" class="mt-0.5 text-xs text-red-500">
        {{ errors.phone }}
      </p>
    </div>

    <div>
      <label class="block text-xs font-medium text-gray-500 mb-1">
        Email
      </label>
      <input
        v-model="email"
        type="email"
        class="block w-full border-b border-[#d4dde5] focus:border-[#4a637a]
               outline-none py-1.5 text-sm"
      />
      <p v-if="errors.email" class="mt-0.5 text-xs text-red-500">
        {{ errors.email }}
      </p>
    </div>

   
    <div class="mt-4">
      <div ref="recaptchaRef"></div>
      <p v-if="recaptchaError" class="mt-1 text-xs text-red-500">
        {{ recaptchaError }}
      </p>
    </div>

    <div class="pt-1">
      <button
        type="submit"
        class="w-full rounded-md bg-[#38566e] text-white text-sm font-semibold
               py-2.5 hover:brightness-110 transition"
      >
        Register Now
      </button>
    </div>
  </form>
</template>
