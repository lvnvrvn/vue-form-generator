<template>
  <div class="field">
    <select :value="modelValue" @change="handleChange">
      <option disabled value="">Выберите страну</option>

      <option v-for="option in obj.options" :key="option" :value="option">
        {{ option }}
      </option>
    </select>

    <p v-if="error" class="error">
      {{ error }}
    </p>
  </div>
</template>

<script setup>
const props = defineProps({
  obj: Object,
  modelValue: String,
  error: String,
});

const emit = defineEmits(["update:modelValue"]);

function handleChange(event) {
  emit("update:modelValue", event.target.value);
}
</script>
