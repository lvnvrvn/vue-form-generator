<template>
  <BaseInput
    v-if="
      obj.type === 'text' || obj.type === 'email' || obj.type === 'password'
    "
    :obj="obj"
    :error="error"
    v-model="model"
  />

  <SelectField
    v-else-if="obj.type === 'select'"
    :obj="obj"
    :error="error"
    v-model="model"
  />

  <CheckboxField
    v-else-if="obj.type === 'checkbox'"
    :obj="obj"
    :error="error"
    v-model="model"
  />
</template>

<script setup>
import { computed } from "vue";

import BaseInput from "./BaseInput.vue";
import SelectField from "./SelectField.vue";
import CheckboxField from "./CheckboxField.vue";

const props = defineProps({
  obj: Object,
  modelValue: [String, Boolean],
  error: String,
});

const emit = defineEmits(["update:modelValue"]);

const componentMap = {
  text: BaseInput,
  password: BaseInput,
  email: BaseInput,
  select: SelectField,
  checkbox: CheckboxField,
};

const model = computed({
  get() {
    return props.modelValue;
  },

  set(value) {
    emit("update:modelValue", value);
  },
});
</script>
