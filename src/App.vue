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
    placeholder: "Введите имя",
    model: "name",
    rules: ["required", "min:3"],
  },

  {
    id: 1,
    type: "email",
    placeholder: "Введите email",
    model: "email",

    rules: ["required", "email"],
  },

  {
    id: 2,
    type: "password",
    placeholder: "Введите пароль",
    model: "password",
    rules: ["required", "min:6"],
  },

  {
    id: 3,
    type: "select",
    model: "country",
    rules: ["required"],

    options: ["Germany", "France", "USA"],
  },

  {
    id: 4,
    type: "checkbox",
    model: "terms",
    rules: ["required"],
  },
];

// const formData = reactive({
//   name: "",
//   email: "",
//   password: "",
//   country: "",
//   terms: false,
// });

const formData = ref({
  name: "",
  email: "",
  password: "",
  country: "",
  terms: false,
});
</script>
