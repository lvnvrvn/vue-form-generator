<template>
  <label>
    <input type="checkbox" :checked="modelValue" @change="handleChange" />

    Принять условия
  </label>
</template>

<script setup>
const props = defineProps({
  modelValue: Boolean,
});

const emit = defineEmits(["update:modelValue"]);

function handleChange(event) {
  emit("update:modelValue", event.target.checked);
}
</script>
