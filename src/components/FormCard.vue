<template>
  <FlipCard :flipped="isTipActive">
    <VCard>
      <form class="form" action="" @submit.prevent>
        <VHeading level="3">Сообщение в свободной форме</VHeading>
        <TextField
          id="name-input"
          placeholder="Ваше имя"
          :model-value="modelValue.name"
          @update:modelValue="updateModelValue('name', $event)"
        />
        <TextField
          id="company-input"
          placeholder="Компания"
          :model-value="modelValue.company"
          @update:modelValue="updateModelValue('company', $event)"
        />
        <TextField
          id="phone-input"
          placeholder="Телефон"
          :model-value="modelValue.phone"
          @update:modelValue="updateModelValue('phone', $event)"
        />
        <TextField
          id="email-input"
          placeholder="Электронная почта"
          :model-value="modelValue.email"
          @update:modelValue="updateModelValue('email', $event)"
        />
        <MultilineField
          id="message-input"
          placeholder="Напишите текст обращения"
          :model-value="modelValue.message"
          :disabled="!!modelValue.file"
          @update:modelValue="updateModelValue('message', $event)">
          <template #icon>
            <IconInformer @click="isTipActive = true"/>
          </template>
          <template #append>
            <FileField
              id="file-input"
              :model-value="modelValue.file"
              label="или прикрепите файл"
              @update:modelValue="updateModelValue('file', $event)"
              :disabled="!!modelValue.message"
            />
          </template>
        </MultilineField>
        <div class="form__group form__group--offset-top">
          <CheckboxField
            id="agreement-input"
            :model-value="modelValue.agreement"
            @update:modelValue="updateModelValue('agreement', $event)"
          >
            согласен на обработку моих <br> <a class="form__personal" href="#">персональных данных</a>
          </CheckboxField>
          <VButton :disabled="!isFormValid">
            Отправить
          </VButton>
        </div>
      </form>
    </VCard>
    <VCard>
      <VHeading level="2" bottom-offset>Что написать в сообщении или файле?</VHeading>
      <TipList>
        <TipListItem v-for="(tip, i) in tips" :title="`${i+1}. ${tip.title}`" :text="tip.text"/>
      </TipList>
      <VButton class="tip-back-button" @click="isTipActive = false">
        <IconArrowBack/>
        Вернуться к заполнению
      </VButton>
    </VCard>
  </FlipCard>
</template>

<script setup lang="ts">
import VCard from "@/components/base/VCard.vue";
import VHeading from "@/components/typography/VHeading.vue";
import TextField from "@/components/form/TextField.vue";
import type {Form} from "@/App.vue";
import {ref, toRaw} from "vue";
import MultilineField from "@/components/form/MultilineField.vue";
import IconInformer from "@/components/icons/IconInformer.vue";
import FileField from "@/components/form/FileField.vue";
import CheckboxField from "@/components/form/CheckboxField.vue";
import VButton from "@/components/base/VButton.vue";
import TipList from "@/components/TipList.vue";
import TipListItem from "@/components/TipListItem.vue";
import FlipCard from "@/components/FlipCard.vue";
import IconArrowBack from "@/components/icons/IconArrowBack.vue";

const tips = [
  {
    title: 'Чем вы занимаетесь?',
    text: `Расскажите о своей компании.\nКак работаете, на чем зарабатываете?\nКто ваши конкуренты?\nЧем вы от них отличаетесь?`
  },
  {
    title: 'В чем ваша задача?',
    text: `Чего хотите достичь в ближайшем будущем\nЧто вам мешает?`
  },
  {
    title: 'Каким вы видите решение задачи?',
    text: `Как планируете достичь своих целей?\nКакие решения пробовали раньше?`
  },
  {
    title: 'Какие у вас ожидания от результата?',
    text: `В каком виде вы хотите видеть решение вашей задачи?\nВ какой срок?\nПочему он важен?\nНа что это должно быть похоже?`
  },
  {
    title: 'Сколько денег планируете потратить?',
    text: `Каков ваш бюджет?\nПочему вы готовы потратить именно такую сумму?`
  },
]

export interface Props {
  modelValue: Form;
  isFormValid: boolean;
}

type Emits = (e: 'update:modelValue', val: Form) => void;

const props = defineProps<Props>();
const emit = defineEmits<Emits>();

const isTipActive = ref(false);

function updateModelValue<T extends keyof Form>(field: T, value: Form[T]) {
  const _form = structuredClone(toRaw(props.modelValue));
  _form[field] = value;
  emit('update:modelValue', _form);
}
</script>

<style scoped>
.form .form__group {
    display: flex;
    gap: 20px;
}

.form .form__group * {
    flex: 1;
}

.form .form__group.form__group--offset-top {
    margin-top: 60px;
}

.form .form__personal {
    color: #05AC6A;
    cursor: pointer;
    text-decoration: none;
}

.tip-back-button {
    margin: 42px auto 0;
}
</style>
