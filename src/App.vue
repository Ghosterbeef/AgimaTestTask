<template>
  <main>
    <VHeading>Анкета для новых клиентов AGIMA</VHeading>
    <FormCard v-model="model" :is-form-valid="isFormValid"/>
  </main>
</template>

<script setup lang="ts">
import VHeading from '@/components/typography/VHeading.vue';
import FormCard from "@/components/FormCard.vue";
import {computed, ref} from "vue";

export interface Form {
  name: string;
  company: string;
  phone: string;
  email: string;
  message: string;
  file: File | null;
  agreement: boolean;
}

const model = ref({
  name: '',
  company: '',
  phone: '',
  email: '',
  message: '',
  file: null,
  agreement: false,
});

const isFormValid = computed(() => {
  return !!(
    model.value.name
    && model.value.company
    && model.value.phone
    && model.value.email
    && model.value.agreement
    && (model.value.file || model.value.message)
  )
})
</script>
