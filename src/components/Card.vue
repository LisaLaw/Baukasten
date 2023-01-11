<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref } from "vue";
import plus from "@/assets/icons/user-plus.svg";
import Color from "@/components/Color.vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

const colors = ref([]);
</script>

<template>
  <div class="card">
    <button class="plusBtn">
      <img :src="plus" />
    </button>
    <div v-for="(color, index) in colors" :key="index">
      <Color :color="color"></Color>
    </div>
    <h2>{{ props.name }}</h2>
  </div>
</template>
