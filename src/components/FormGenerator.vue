<template>
  <form @submit.prevent="handleSubmit">
    <div v-for="obj in props.schema" :key="obj.id">
      <FormField
        :obj="obj"
        v-model="model[obj.model]"
        :error="errors[obj.model]"
      />
    </div>

    <button>Отправить</button>
  </form>
</template>

<script setup>
import { reactive, computed } from "vue";
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
        errors[obj.model] = `Минимум ${min} символа`;
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

function handleSubmit() {
  console.log(errors);

  props.schema.forEach((obj) => {
    validateField(obj);
  });

  if (Object.keys(errors).length > 0) {
    return;
  }

  console.log(model);

  alert("Форма отправлена");
}
</script>
