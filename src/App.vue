<template>
  <MyForm
    :initial-values="formObject"
    :errors="errors"
    @update="updateHandler"
  />
  <View :form-object="formObject" />
  <button :disabled="!valid">submit</button>
</template>

<script lang="ts">
import MyForm from "./components/MyForm.vue"
import View from "./components/View.vue"
import { defineComponent, computed } from "vue"
import type { FormSchema } from "."
import { useForm } from "vee-validate"
import { object, string } from "yup"

export default defineComponent({
  components: {
    MyForm,
    View,
  },
  setup() {
    const {
      values: formObject,
      errors,
      validate,
      setValues,
      meta,
    } = useForm<FormSchema>({
      validationSchema: object({
        item1: string().defined(),
        item2: string().defined(),
        item3: string().required(),
      }),
      initialValues: {
        item1: "",
        item2: "",
        item3: "",
      },
    })

    const updateHandler = async (form: FormSchema) => {
      setValues(form)
      await validate()
    }

    const valid = computed(() => meta.value.valid)

    return {
      formObject,
      errors,
      updateHandler,
      valid,
    }
  },
})
</script>
