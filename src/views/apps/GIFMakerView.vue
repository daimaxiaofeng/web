<script setup>
import { reactive, ref } from 'vue'
import { mdiBallotOutline, mdiAccount, mdiMail, mdiGithub } from '@mdi/js'
import SectionMain from '@/components/SectionMain.vue'
import CardBox from '@/components/CardBox.vue'
import FormCheckRadioGroup from '@/components/FormCheckRadioGroup.vue'
import FormFilePicker from '@/components/FormFilePicker.vue'
import FormField from '@/components/FormField.vue'
import FormControl from '@/components/FormControl.vue'
import BaseDivider from '@/components/BaseDivider.vue'
import BaseButton from '@/components/BaseButton.vue'
import BaseButtons from '@/components/BaseButtons.vue'
import SectionTitle from '@/components/SectionTitle.vue'
import LayoutAuthenticated from '@/layouts/LayoutAuthenticated.vue'
import SectionTitleLineWithButton from '@/components/SectionTitleLineWithButton.vue'
import NotificationBarInCard from '@/components/NotificationBarInCard.vue'

const selectOptions = [
  { id: 1, label: '王境泽真香', inputCount: 4, placeholders: {
    1: "我就是饿死",
    2: "死外边 从这跳下去",
    3: "也不会吃你们一点东西",
    4: "真香"
  } },
  // { id: 2, label: 'sorry', inputCount: 1, placeholders: {
  //   1: ""
  // } },
  // { id: 3, label: 'diandongche', inputCount: 1, placeholders: {
  //   1: ""
  // } },
  // { id: 4, label: 'kongming', inputCount: 1, placeholders: {
  //   1: ""
  // } },
  // { id: 5, label: 'dagong', inputCount: 1, placeholders: {
  //   1: ""
  // } },
  // { id: 6, label: 'marmot', inputCount: 1, placeholders: {
  //   1: ""
  // } },
  // { id: 7, label: 'jinkala', inputCount: 1, placeholders: {
  //   1: ""
  // } }
]

const form = reactive({
  name: 'John Doe',
  email: 'john.doe@example.com',
  phone: '',
  department: selectOptions[0],
  subject: '',
  question: ''
})

const customElementsForm = reactive({
  checkbox: ['lorem'],
  radio: 'one',
  switch: ['one'],
  file: null
})

const submit = () => {
  //
}

const formStatusWithHeader = ref(true)

const formStatusCurrent = ref(0)

const formStatusOptions = ['info', 'success', 'danger', 'warning']

const Submit = () => {
  formStatusCurrent.value = formStatusOptions[formStatusCurrent.value + 1]
    ? formStatusCurrent.value + 1
    : 0
}
</script>

<template>
  <LayoutAuthenticated>
    <SectionMain>
      <SectionTitleLineWithButton :icon="mdiBallotOutline" title="GIF 表情包制作" main>
      </SectionTitleLineWithButton>
      <!-- <CardBox form @submit.prevent="Submit"> -->
      <CardBox
      is-form
      is-hoverable
      @submit.prevent="Submit"
      >
        <NotificationBarInCard
          :color="formStatusOptions[formStatusCurrent]"
          :is-placed-with-header="formStatusWithHeader"
        >
          <span
            ><b class="capitalize">{{ formStatusOptions[formStatusCurrent] }}</b> state</span
          >
        </NotificationBarInCard>

        <FormField label="模板">
          <FormControl v-model="form.department" :options="selectOptions" />
        </FormField>

        <BaseDivider />

        <template v-for="index in form.department.inputCount" :key="index">
          <FormField :label="`第 ${index} 句`">
            <FormControl :placeholder="`${form.department.placeholders[index]}`" />
          </FormField>
        </template>


        <template #footer>
          <BaseButtons>
            <BaseButton type="formStatusSubmit" color="info" label="制作" />
            <BaseButton type="reset" color="info" outline label="重置" />
          </BaseButtons>
        </template>
      </CardBox>
    </SectionMain>

  </LayoutAuthenticated>
</template>