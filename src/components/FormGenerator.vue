<template>
  <form @submit.prevent="handleSubmit">
    <div v-for="obj in props.schema" :key="obj.id">
      <FormField
        :obj="obj"
        :error="errors[obj.model]"
        v-model="model[obj.model]"
        @validate="validateField(obj)"
      />
    </div>

    <button :disabled="!isFormValid">Отправить</button>

    <p v-if="submitted" class="success">Форма успешно отправлена!</p>
  </form>
</template>

<script setup>
import { reactive, computed, ref } from "vue";
import FormField from "./FormField.vue";

const props = defineProps({
  schema: Array,
  modelValue: Object,
});

const emit = defineEmits(["update:modelValue"]);

const model = computed({
  get() {
    return props.modelValue;
  },

  set(value) {
    emit("update:modelValue", value);
  },
});

const errors = reactive({});

function validateField(obj) {
  delete errors[obj.model];

  const value = model.value[obj.model];

  for (const rule of obj.rules) {
    if (rule === "required") {
      if (obj.type === "checkbox" ? !value : !String(value).trim()) {
        errors[obj.model] = "Поле обязательно";
        return;
      }
    }

    if (rule.startsWith("min:")) {
      const min = Number(rule.split(":")[1]);

      if (String(value).length < min) {
        errors[obj.model] = `Минимум ${min} ${getSymbolWord(min)}`;
        return;
      }
    }

    if (rule === "email") {
      if (!value) return;

      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

      if (!emailRegex.test(value)) {
        errors[obj.model] = "Некорректный email";
        return;
      }
    }
  }
}

function getSymbolWord(count) {
  if (count === 1) {
    return "символ";
  }

  if (count >= 2 && count <= 4) {
    return "символа";
  }

  return "символов";
}

function handleSubmit() {
  props.schema.forEach((obj) => {
    validateField(obj);
  });

  if (Object.keys(errors).length > 0) {
    return;
  }

  if (Object.keys(errors).length === 0) {
    submitted.value = true;
  }

  Object.keys(model.value).forEach((key) => {
    if (typeof model.value[key] === "boolean") {
      model.value[key] = false;
    } else {
      model.value[key] = "";
    }
  });

  Object.keys(errors).forEach((key) => {
    delete errors[key];
  });
}

const isFormValid = computed(() => Object.keys(errors).length === 0);
const submitted = ref(false);
</script>
