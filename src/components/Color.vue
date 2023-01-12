<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref } from "vue";
import edit from "@/assets/icons/edit.svg";
import deleteImg from "@/assets/icons/delete.svg";

const props = defineProps({
  color: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits("color-deleted", "color-edited");

const newColor = ref(props.color);

const onDelete = () => emit("color-deleted", newColor);
const onEdit = () => emit("color-edited", newColor);
</script>

<template v-if="newColor.length">
  <div
    v-if="!color.isInputVisible"
    class="color"
    :style="{
      backgroundColor: newColor.value,
    }"
  >
    <p>{{ newColor.name }}</p>
    <div>
      <button type="button" @click="onEdit">
        <img :src="edit" />
      </button>
      <button type="button" @click="onDelete">
        <img :src="deleteImg" />
      </button>
    </div>
  </div>
</template>
