<script setup>
import { ref } from "vue";

const newName = ref("");

const emit = defineEmits(["person-submitted"]);

const onSubmit = () => {
  emit("person-submitted", newName.value);
  newName.value = "";
};
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input id="name" v-model="newName" placeholder="Name der Person" />

    <input class="button" type="submit" value="Hinzufügen" />
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>
