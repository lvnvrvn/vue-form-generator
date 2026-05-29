<template>
  <form @submit.prevent="handleSubmit">
    <div v-for="obj in arrOfObjs" :key="obj.id">
      <FormField
        :obj="obj"
        v-model="formData[obj.model]"
        :error="errors[obj.model]"
      />
    </div>

    <button>Отправить</button>
  </form>

  <hr />

  {{ formData }}
</template>

<script setup>
import { reactive } from "vue";
import FormField from "./components/FormField.vue";

const arrOfObjs = [
  {
    id: 0,
    type: "text",
    placeholder: "Введите имя",
    model: "name",
    rules: ["required", "min:3"],
  },

  {
    id: 1,
    type: "password",
    placeholder: "Введите пароль",
    model: "password",
    rules: ["required", "min:6"],
  },

  {
    id: 2,
    type: "select",
    model: "country",
    rules: ["required"],

    options: ["Germany", "France", "USA"],
  },

  {
    id: 3,
    type: "checkbox",
    model: "terms",
    rules: ["required"],
  },

  {
    id: 4,
    type: "email",
    placeholder: "Введите email",
    model: "email",

    rules: ["required", "email"],
  },
];

const formData = reactive({
  name: "",
  password: "",
  country: "",
  terms: false,
});

const errors = reactive({});

function validateField(obj) {
  delete errors[obj.model];

  const value = formData[obj.model];

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
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

      if (!emailRegex.test(value)) {
        errors[obj.model] = "Некорректный email";

        return;
      }
    }
  }
}

function handleSubmit() {
  arrOfObjs.forEach((obj) => {
    validateField(obj);
  });

  if (Object.keys(errors).length > 0) {
    alert("Форма заполнена неправильно");
    return;
  }

  console.log(formData);

  alert("Форма отправлена");
}
</script>
