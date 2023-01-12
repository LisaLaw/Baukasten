<script setup>
import { ref, onMounted } from "vue";

const props = defineProps({
  oldColor: {
    type: Object,
  },
});

const emit = defineEmits("color-selected");

const availableColors = ref([]);
const newColor = ref();

onMounted(() => {
  fetch("http://localhost:3000/colors")
    .then((response) => response.json())
    .then((data) => (availableColors.value = data));
});

const onSelect = () => emit("color-selected", newColor, props.oldColor);
</script>

<template>
  <select v-model="newColor" @change="onSelect">
    <option
      v-for="(color, index) in availableColors"
      :key="index"
      :value="color"
    >
      {{ color.name }}
    </option>
  </select>
</template>
