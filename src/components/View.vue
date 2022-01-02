<template>
  <div class="form-item-container">
    <div class="form-item">
      <label for="item1">Item1</label>
      <p>{{ formObject.item1 }}</p>
    </div>
    <div class="form-item">
      <label for="item2">Item2</label>
      <p>{{ formObject.item2 }}</p>
    </div>
    <div class="form-item">
      <label for="item3">Item3</label>
      <p>{{ formObject.item3 }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue"
import type { FormSchema } from "../index"

export default defineComponent({
  props: {
    formObject: {
      type: Object as PropType<FormSchema>,
      required: true,
    },
  },
})
</script>

<style scoped>
p {
  margin: 0;
}
.form-item-container {
  display: grid;
  gap: 0.5rem;
  margin-top: 1.5rem;
}

.form-item {
  display: flex;
  gap: 1rem;
}
</style>
