<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import edit from "@/assets/icons/edit.svg";
import deleteImg from "@/assets/icons/delete.svg";

const props = defineProps({
  color: {
    type: Object,
    required: true,
  },
});

const emit = defineEmits("color-deleted", "color-edited");

const onDelete = () => emit("color-deleted");
const onEdit = () => emit("color-edited", props.color);
</script>

<template v-if="props.color.length">
  <div
    v-if="!color.isInputVisible"
    class="color"
    :style="{
      backgroundColor: props.color.value,
    }"
  >
    <p>{{ props.color.name }}</p>
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
