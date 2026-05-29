<template>
  <div class="field">
    <label>
      {{ obj.label }}
    </label>

    <textarea
      v-if="obj.type === 'textarea'"
      :placeholder="obj.placeholder"
      :value="modelValue"
      :class="{ 'error-input': error }"
      @input="handleInput"
    />

    <input
      v-else
      :type="obj.type"
      :placeholder="obj.placeholder"
      :value="modelValue"
      :class="{ 'error-input': error }"
      @input="handleInput"
    />

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

function handleInput(event) {
  emit("update:modelValue", event.target.value);
}
</script>
