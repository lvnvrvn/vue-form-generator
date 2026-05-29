<template>
  <FormGenerator :schema="formSchema" v-model="formData" />
</template>

<script setup>
import { reactive, ref } from "vue";
import FormGenerator from "./components/FormGenerator.vue";

const formSchema = [
  {
    id: 0,
    type: "text",
    label: "Имя",
    placeholder: "Введите имя",
    model: "name",
    rules: ["required", "min:3"],
  },

  {
    id: 1,
    type: "email",
    label: "Email",
    placeholder: "Введите email",
    model: "email",

    rules: ["required", "email"],
  },

  {
    id: 2,
    type: "password",
    label: "Пароль",
    placeholder: "Введите пароль",
    model: "password",
    rules: ["required", "min:6"],
  },

  {
    id: 3,
    type: "select",
    label: "Страна",
    model: "country",
    rules: ["required"],

    options: ["Germany", "France", "USA"],
  },

  {
    id: 4,
    type: "checkbox",
    label: "Согласие с условиями",
    model: "terms",
    rules: ["required"],
  },

  {
    id: 5,
    type: "textarea",
    label: "О себе",
    placeholder: "Расскажите о себе",
    model: "about",

    rules: ["required", "min:10"],
  },
];

const formData = ref({
  name: "",
  email: "",
  password: "",
  country: "",
  terms: false,
  about: "",
});
</script>
