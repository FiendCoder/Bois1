<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { useForm, useField } from 'vee-validate'
import * as yup from 'yup'

const RECAPTCHA_SITE_KEY = '6LdTTBAsAAAAADUmBpbxdUPUlxVlc6garM3_68kk' 

const emit = defineEmits<{
  (e: 'submitted', payload: any): void
}>()

const schema = yup.object({
  firstName: yup.string().required('First name is required'),
  lastName: yup.string().required('Last name is required'),
  email: yup.string().email('Enter a valid email').required('Email is required'),
  phone: yup.string().required('Phone is required'),
  message: yup.string().optional(),
  recaptchaToken: yup
    .string()
    .required('Please confirm you are not a robot'),
})

const {
  handleSubmit,
  errors,
  setFieldValue,
} = useForm({
  validationSchema: schema,
})

const { value: firstName } = useField<string>('firstName')
const { value: lastName } = useField<string>('lastName')
const { value: email } = useField<string>('email')
const { value: phone } = useField<string>('phone')
const { value: message } = useField<string>('message')


const recaptchaContainer = ref<HTMLElement | null>(null)
let widgetId: number | null = null

const updateRecaptchaToken = (token: string) => {
  setFieldValue('recaptchaToken', token)
}

onMounted(() => {
  // @ts-ignore grecaptcha is injected globally from index.html
  if (window.grecaptcha && recaptchaContainer.value) {
    // @ts-ignore
    widgetId = window.grecaptcha.render(recaptchaContainer.value, {
      sitekey: RECAPTCHA_SITE_KEY,
      callback: (token: string) => updateRecaptchaToken(token),
      'expired-callback': () => updateRecaptchaToken(''),
      'error-callback': () => updateRecaptchaToken(''),
    })
  }
})

onBeforeUnmount(() => {
  // @ts-ignore
  if (widgetId !== null && window.grecaptcha) {
    // @ts-ignore
    window.grecaptcha.reset(widgetId)
  }
})

const onSubmit = handleSubmit(values => {

  emit('submitted', values)
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
        How can Ben help you?
      </label>
      <textarea
        v-model="message"
        rows="3"
        class="block w-full border border-[#d4dde5] focus:border-[#4a637a]
               outline-none py-1.5 px-2 text-sm resize-none"
      />
      <p v-if="errors.message" class="mt-0.5 text-xs text-red-500">
        {{ errors.message }}
      </p>
    </div>

    
    <div>
      <div ref="recaptchaContainer"></div>
      <p v-if="errors.recaptchaToken" class="mt-0.5 text-xs text-red-500">
        {{ errors.recaptchaToken }}
      </p>
    </div>

    <div class="pt-1">
      <button
        type="submit"
        class="w-full rounded bg-[#38566e] text-white text-sm font-semibold
               py-2.5 hover:brightness-110 transition"
      >
        Connect Now
      </button>
    </div>
  </form>
</template>
