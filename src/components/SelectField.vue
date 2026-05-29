<template>
  <select :value="modelValue" @change="handleChange">
    <option disabled value="">Выберите страну</option>

    <option v-for="option in obj.options" :key="option" :value="option">
      {{ option }}
    </option>
  </select>
</template>

<script setup>
const props = defineProps({
  obj: Object,
  modelValue: String,
});

const emit = defineEmits(["update:modelValue"]);

function handleChange(event) {
  emit("update:modelValue", event.target.value);
}
</script>
