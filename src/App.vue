<script setup>
import { ref } from "vue";
import logo from "@/assets/icons/logo.svg";
import deleteImg from "@/assets/icons/delete.svg";
import EntryForm from "@/components/EntryForm.vue";
import Card from "@/components/Card.vue";

const persons = ref(["lisa"]);
const isActive = ref(false);

const addPerson = (newPerson) => {
  if (isActive.value === true) {
    isActive.value = false;
  }
  if (!persons.value.includes(newPerson) && newPerson !== "") {
    persons.value.push(newPerson);
  } else {
    isActive.value = true;
  }
};

const onDelete = (person) => {
  persons.value = persons.value.filter((p) => p !== person);
};
</script>

<template>
  <div class="wrapper">
    <div>
      <img :src="logo" :style="{ height: '140px' }" />
      <EntryForm @person-submitted="addPerson"></EntryForm>
      <p :class="{ isActive: isActive }">Nope, please try again.</p>
    </div>
    <div v-for="person in persons" :key="person" class="card outer">
      <Card :name="person"></Card>
      <button type="button" @click="onDelete(person)">
        <img :src="deleteImg" />
      </button>
    </div>
  </div>
</template>

<style scoped>
p {
  display: none;
}

.isActive {
  display: flex;
  color: red;
  font-weight: bold;
  background-color: lightgray;
  border-radius: 4px;
}
</style>
