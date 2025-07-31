<script setup lang="ts">
import { ref } from 'vue';

import GeneratorSection from './GeneratorSection.vue';

const isGenerator = ref(false);

function displayGenerator() {
    isGenerator.value = true;
}
</script>

<template>
<h1>Hello !</h1>
  <nav class="navigation">
    <ul>
      <li>
        <button @click="displayIdPage">
          Identifiants
        </button>
      </li>
      <li>
        <button @click="displayIdCreation">
          Créer un identifiant
        </button>
      </li>
      <li>
        <button @click="displayGenerator">
          Générer un mot de passe
        </button>
      </li>
    </ul>
  </nav>
  <GeneratorSection v-if="isGenerator" :isGenerator=true />
</template>

<style scoped>
ul {
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

li {
  list-style-type: none;
}
</style>