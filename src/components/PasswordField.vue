<template>
  <input
    type="password"
    :placeholder="obj.placeholder"
    :value="modelValue"
    @input="handleInput"
  />
</template>

<script setup>
const props = defineProps({
  obj: Object,
  modelValue: String,
});

const emit = defineEmits(["update:modelValue"]);

function handleInput(event) {
  emit("update:modelValue", event.target.value);
}
</script>
