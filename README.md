# Vue Form Generator

Динамический генератор форм на Vue 3, который строит форму на основе JSON-схемы.

## Demo

Live demo:

## Возможности

- Динамический рендеринг формы по schema
- Поддержка полей:
  - text
  - email
  - password
  - textarea
  - select
  - checkbox

- Валидация:
  - required
  - min length
  - email validation

- Live validation
- Success state после отправки формы
- Responsive layout
- Переиспользуемые компоненты

## Архитектура

Для текстовых полей используется единый `BaseInput` компонент, что позволяет избежать дублирования логики и упрощает масштабирование системы.

Форма полностью управляется через JSON schema, благодаря чему компонент `FormGenerator` можно переиспользовать для различных сценариев.

## Технологии

- Vue 3
- Composition API
- Vite

## Установка и запуск

```bash
npm install
npm run dev
```

## Пример schema

```js
const formSchema = [
  {
    type: "text",
    label: "Имя",
    placeholder: "Введите имя",
    model: "name",

    rules: ["required", "min:3"],
  },

  {
    type: "email",
    label: "Email",
    placeholder: "Введите email",
    model: "email",

    rules: ["required", "email"],
  },
];
```

## Структура проекта

```txt
src/
├── components/
│   ├── BaseInput.vue
│   ├── SelectField.vue
│   ├── CheckboxField.vue
│   ├── FormField.vue
│   └── FormGenerator.vue
│
├── assets/
│   └── styles.css
│
├── App.vue
└── main.js
```
