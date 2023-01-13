<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref } from "vue";
import Color from "@/components/Color.vue";
import ColorSelector from "./ColorSelector.vue";
import plus from "@/assets/icons/user-plus.svg";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
});

const chosenColors = ref([
  {
    name: "Gelb",
    value: "#fffb9b",
  },
  {
    name: "Blau",
    value: "#a1d7f4",
  },
]);

const selectedColor = ref();

const addColor = (newColor) => {
  chosenColors.value = [...chosenColors.value, newColor.value];
};

const deleteColor = (index) => {
  chosenColors.value.splice(index, 1);
};

const editColor = (colorToEdit) => {
  colorToEdit.isInputVisible = true;
};

const changeColor = (selected, oldColor) => {
  selectedColor.value = selected.value;
  selectedColor.value.isInputVisible = false;
  const colorToReplace = chosenColors.value.findIndex((el) => el === oldColor);
  chosenColors.value[colorToReplace] = selectedColor.value;
};
</script>

<template>
  <div class="card">
    <ColorSelector
      @color-selected="addColor"
      class="topSelector"
      :selector-image="true"
    >
    </ColorSelector>
    <img :src="plus" class="selectorImg" />
    <div v-for="(color, index) in chosenColors" :key="index">
      <Color
        v-if="!color.isInputVisible"
        :color="color"
        @color-deleted="deleteColor(index)"
        @color-edited="editColor(color)"
        :index="index"
      ></Color>
      <div v-else>
        <ColorSelector
          @color-selected="changeColor"
          :oldColor="color"
        ></ColorSelector>
      </div>
    </div>
    <h2>{{ props.name }}</h2>
  </div>
</template>
