<script setup lang="ts">
import { ref } from "vue";

const props = defineProps<{
  isGenerator: boolean;
  length: string;
}>();

const numberChosen = ref(false);
const specialCharsChosen = ref(false);
const pickedLength = ref("");

function randomisePassword(length: string): string {
  let result = [];
  let chars = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
  let numbers = "0123456789";
  let specialChars = 'éèçà!è§(&@-_)#@êëù%$*€`£=+/:.;?,âäûüîïôö"';
  for (let i = 0; i < +length; i++) {
    if (numberChosen.value) {
      const setOfChars = chars + numbers;
      result.push(
        setOfChars.charAt(Math.floor(Math.random() * +setOfChars.length)),
      );
    } else if (specialCharsChosen.value) {
      const setOfChars = chars + specialChars;
      result.push(
        setOfChars.charAt(Math.floor(Math.random() * +setOfChars.length)),
      );
    } else if (numberChosen && specialCharsChosen) {
      const setOfChars = chars + numbers + specialChars;
      result.push(
        setOfChars.charAt(Math.floor(Math.random() * +setOfChars.length)),
      );
    }
  }
  return result.join("");
}

function displayGeneratedPassword(length: string) {
  return randomisePassword(length);
}
</script>

<template>
  <div class="what-to-include">
    <p>Include</p>
    <div class="can-include">
      <label for="characters">characters</label>
      <input type="checkbox" value="Characters" id="characters" checked="" />
      <label for="numbers">numbers</label>
      <input type="checkbox" value="Numbers" id="numbers" />
      <label for="special-chars">special characters</label>
      <input type="checkbox" value="Special characters" id="special-chars" />
    </div>
  </div>
  <p>Value must be between 8 and 128</p>
  <label for="length">Length</label>
  <input type="number" v-model="pickedLength" id="length" name="length" />
  <p class="display-password">
    {{ displayGeneratedPassword(pickedLength) }}
  </p>
</template>

<style scoped>
.what-to-include {
  width: 50%;
  margin: auto;
}
</style>
