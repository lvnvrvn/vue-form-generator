<template>
  <div class="field">
    <textarea
      v-if="obj.type === 'textarea'"
      :placeholder="obj.placeholder"
      :value="modelValue"
      @input="handleInput"
    />

    <input
      v-else
      :type="obj.type"
      :placeholder="obj.placeholder"
      :value="modelValue"
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
