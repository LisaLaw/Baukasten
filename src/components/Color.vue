<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { computed } from "vue";
import edit from "@/assets/icons/edit.svg";
import deleteImg from "@/assets/icons/delete.svg";

const props = defineProps({
  color: {
    type: Object,
    required: true,
  },
});

const newColor = computed(() => props.color);
</script>

<template>
  <div class="color" :style="{ backgroundColor: newColor.value }">
    <p>{{ newColor.name }}</p>
    <div>
      <img :src="edit" />
      <img :src="deleteImg" />
    </div>
  </div>
</template>
