<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { computed } from "vue";

const newColor = computed(() => console.log("testing color"));
</script>

<template>
  <div>{{ newColor }}</div>
</template>
