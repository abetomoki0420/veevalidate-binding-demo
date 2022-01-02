<template>
  <h1>My form component</h1>
  <div class="form-item-container">
    <div class="form-item">
      <label for="item1">Item1</label>
      <input v-model="form.item1" id="item1" type="text" />
    </div>
    <div class="form-item">
      <label for="item2">Item2</label>
      <input v-model="form.item2" id="item2" type="text" />
    </div>
    <div class="form-item">
      <label for="item3">Item3</label>
      <input v-model="form.item3" id="item3" type="text" />
      <div v-if="errors">
        <template v-if="errors['item3']">
          {{ errors["item3"] }}
        </template>
      </div>
    </div>
</template>

<script lang="ts">
import { defineComponent, PropType, ref, watch } from "vue"
import type { FormSchema } from "../index"

export default defineComponent({
  props: {
    initialValues: {
      type: Object as PropType<FormSchema>,
      required: true,
    },
    errors: {
      type: Object as PropType<Partial<Record<keyof FormSchema, string>>>,
    },
  },
  emits: ["update"],
  setup(props, { emit }) {
    const form = ref({ ...props.initialValues })

    watch(form.value, () => {
      emit("update", form.value)
    })

    return {
      form,
    }
  },
})
</script>

<style>
.form-item-container {
  display: grid;
  gap: 0.5rem;
}

.form-item {
  display: flex;
  gap: 1rem;
}
</style>
