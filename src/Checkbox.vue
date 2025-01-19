<template>
    <label>
      <input type="checkbox" @change="onChange">
      {{ label }}
    </label>
  </template>
  
  <script setup>

  defineProps({
    label: String,
    checked: Boolean
  });
  
  const emits = defineEmits(['check', 'unchecked']);
  
  const onChange = (event) => {
    if (event.currentTarget.checked) {
      emits('check', event.currentTarget);
    } else {
      emits('unchecked', event.currentTarget);
    }
  };
  </script>  