<script setup lang="ts">
import { ref } from 'vue';

const props = defineProps<{
  isGenerator: boolean,
  length: string,
}>();

const numberChosen = ref(false);
const specialCharsChosen = ref(false);
const pickedLength = ref('');

function randomisePassword(length: string): string {
  let result = []
  let chars = 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
  let numbers = '0123456789';
  let specialChars = 'éèçà!è§(&@-_)#@êëù%$*€`£=+/:.;?,âäûüîïôö'
  for (let i = 0; i < +length; i++) {
    if (numberChosen.value) {
      const setOfChars = chars + numbers;
      result.push(setOfChars.charAt(Math.floor(Math.random() * +length)));
    } else if (specialCharsChosen.value) {
      const setOfChars = chars + specialChars;
      result.push(setOfChars.charAt(Math.floor(Math.random() * +length)));
    } else if (numberChosen && specialCharsChosen) {
      const setOfChars = chars + numbers + specialChars;
      result.push(setOfChars.charAt(Math.floor(Math.random() * +length)));
    }
    console.log(result);
  }
    return result.join('');
}

function displayGeneratedPassword(length: string) {
  return randomisePassword(length);
}
</script>

<template>
  <label for="characters">characters</label>
  <input type="checkbox" value="Characters" id="characters" checked="">
  <label for="numbers">numbers</label>
  <input type="checkbox" value="Numbers" id="numbers">
  <label for="speicla-chars">special characters</label>
  <input type="checkbox" value="Special characters" id="special-chars">
  <input type="range" v-model="pickedLength" min="1" max="255"  list="marks">
  <datalist id="marks">
    <option value="1"></option>
    <option value="2"></option>
    <option value="3"></option>
    <option value="4"></option>
    <option value="5"></option>
    <option value="6"></option>
    <option value="7"></option>
    <option value="8"></option>
    <option value="9"></option>
    <option value="10"></option>
    <option value="11"></option>
    <option value="12"></option>
    <option value="13"></option>
    <option value="14"></option>
    <option value="15"></option>
    <option value="16"></option>
    <option value="17"></option>
    <option value="18"></option>
    <option value="19"></option>
    <option value="20"></option>
  </datalist>
  {{ displayGeneratedPassword(pickedLength) }}
</template>

<style scoped>

</style>