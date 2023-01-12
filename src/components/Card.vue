<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, onMounted } from "vue";
import Color from "@/components/Color.vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

const availableColors = ref([]);
const newColor = ref();
const chosenColors = ref([]);

onMounted(() => {
  fetch("http://localhost:3000/colors")
    .then((response) => response.json())
    .then((data) => (availableColors.value = data));
});

const onAddColor = () => {
  chosenColors.value.push(newColor.value);
};

const deleteColor = (index) => {
  const colorToDelete = chosenColors.value[index];
  console.log(colorToDelete);
  chosenColors.value = chosenColors.value.splice(
    colorToDelete,
    chosenColors.value.length - 1
  );
};
</script>

<template>
  <div class="card">
    <select v-model="newColor" @change="onAddColor">
      <option
        v-for="(color, index) in availableColors"
        :key="index"
        :value="color"
        :selected="color === newColor"
      >
        {{ color.name }}
      </option>
    </select>
    <div v-for="(color, index) in chosenColors" :key="index">
      <Color :color="color" @color-deleted="deleteColor(index)"></Color>
    </div>
    <h2>{{ props.name }}</h2>
  </div>
</template>

<style scoped>
select {
  all: unset;
  background-image: url(../assets/icons/user-plus.svg);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  height: 30px;
}
</style>
