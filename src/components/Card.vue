<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref } from "vue";
import Color from "@/components/Color.vue";
import ColorSelector from "./ColorSelector.vue";

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
  chosenColors.value.push(newColor.value);
};

const deleteColor = (index) => {
  const colorToDelete = chosenColors.value[index];
  chosenColors.value = chosenColors.value.splice(
    colorToDelete,
    chosenColors.value.length - 1
  );
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
    ></ColorSelector>
    <div v-for="(color, index) in chosenColors" :key="index">
      <Color
        v-if="!color.isInputVisible"
        :color="color"
        @color-deleted="deleteColor(index)"
        @color-edited="editColor(color)"
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

<style scoped>
.topSelector {
  all: unset;
  background-image: url(../assets/icons/user-plus.svg);
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  height: 30px;
}
</style>
