<script setup lang="ts">
import { ref } from "vue";

import GeneratorSection from "./GeneratorSection.vue";

const isGenerator = ref(false);

function displayGenerator() {
  isGenerator.value = true;
}
</script>

<template>
  <h1>Bienvenue dans votre coffre</h1>
  <nav class="navigation">
    <ul>
      <li>
        <button @click="displayIdPage">Coffre</button>
      </li>
      <li>
        <button @click="displayIdCreation">+ Créer</button>
      </li>
      <li>
        <button @click="displayGenerator">Générer un mot de passe</button>
      </li>
    </ul>
  </nav>
  <GeneratorSection v-if="isGenerator" :isGenerator="true" />
</template>

<style scoped>
ul {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 1.2rem;
}

li {
  list-style-type: none;
}
</style>
