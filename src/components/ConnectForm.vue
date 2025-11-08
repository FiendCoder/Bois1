<script setup lang="ts">
import { useForm, useField } from 'vee-validate'
import * as yup from 'yup'

const emit = defineEmits<{
  (e: 'submitted', payload: any): void
}>()

const schema = yup.object({
  firstName: yup.string().required('First name is required'),
  lastName: yup.string().required('Last name is required'),
  phone: yup.string().required('Phone is required'),
  email: yup.string().email('Enter a valid email').required('Email is required'),
  consent: yup
    .boolean()
    .oneOf([true], 'Please confirm you are not a robot'),
})

const { handleSubmit, errors } = useForm({
  validationSchema: schema,
})

const { value: firstName } = useField<string>('firstName')
const { value: lastName } = useField<string>('lastName')
const { value: phone } = useField<number>('phone')
const { value: email } = useField<string>('email')
const { value: consent } = useField<boolean>('consent')

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

   
    <div>
      <div
        class="flex items-center justify-between border border-[#d4dde5]
               bg-[#f7f8fa] px-3 py-2"
      >
        <label class="flex items-center gap-2 text-xs text-gray-600">
          <input
            v-model="consent"
            type="checkbox"
            class="w-4 h-4 border border-gray-400"
          />
          <span>I’m not a robot</span>
        </label>
        <div
          class="w-9 h-9 rounded bg-white border border-[#d4dde5]
                 text-[9px] grid place-items-center text-gray-500"
        >
          reCAPTCHA
        </div>
      </div>
      <p v-if="errors.consent" class="mt-0.5 text-xs text-red-500">
        {{ errors.consent }}
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
