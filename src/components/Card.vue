<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, onMounted } from "vue";
import plus from "@/assets/icons/user-plus.svg";
import Color from "@/components/Color.vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

const availableColors = ref([]);
const chosenColors = ref([]);

onMounted(() => {
  fetch("http://localhost:3000/colors")
    .then((response) => response.json())
    .then((data) => (availableColors.value = data));
});

const onAddColor = (color) => {
  console.log(color);
  chosenColors.value.push(color);
  console.log(chosenColors);
};
</script>

<template>
  <div class="card">
    <img :src="plus" />
    <select
      id="colorSelector"
      v-model="chosenColors.value"
      @change="onAddColor(chosenColors)"
    >
      <option
        v-for="(color, index) in availableColors"
        :key="index"
        :value="color"
      >
        {{ color.name }}
      </option>
    </select>
    <div v-for="(color, index) in chosenColors" :key="index">
      <Color :color="color.value"></Color>
    </div>
    <h2>{{ props.name }}</h2>
  </div>
</template>
