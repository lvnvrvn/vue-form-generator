<template>
  <div>
    <label>
      <input type="checkbox" :checked="modelValue" @change="handleChange" />

      Принять условия
    </label>

    <p v-if="error">
      {{ error }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  obj: Object,
  modelValue: Boolean,
  error: String,
});

const emit = defineEmits(["update:modelValue"]);

function handleChange(event) {
  emit("update:modelValue", event.target.checked);
}
</script>
