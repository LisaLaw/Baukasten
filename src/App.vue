<script setup>
import { ref } from "vue";
import logo from "@/assets/icons/logo.svg";
import EntryForm from "@/components/EntryForm.vue";
import Card from "@/components/Card.vue";

const persons = ref(["lisa"]);

const addPerson = (newPerson) => {
  persons.value.push(newPerson);
};
</script>

<template>
  <div class="wrapper">
    <div>
      <img :src="logo" :style="{ height: '140px' }" />
      <EntryForm @person-submitted="addPerson"></EntryForm>
    </div>
    <div v-for="person in persons" :key="person">
      <Card :name="person"></Card>
    </div>
  </div>
</template>
