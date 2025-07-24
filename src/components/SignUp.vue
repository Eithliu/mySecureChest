<script setup>
  import { computed, ref } from 'vue';

  const regex = /^(?=.*?[A-Z])(?=.*?[a-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).*$/
  const userInput = ref('');
  const userReInput = ref('');
  const isInvalidPassword = ref(false);
  const checkPass = computed(() => {
    if (userInput.value !== userReInput.value) {

    }
  })

  const checkValidity = computed(() => {
    if (userInput.value.match(regex)) return;
    return isInvalidPassword.value = true;
  })

  const emit = defineEmits(['click'])

  function click() {
    emit('click');
  }
</script>

<template>
  <p>Créer un mot de passe maître.</p>
  <label for="type-password"></label>
  <input type="password" v-model="userInput" name="type-password" @focusout="checkValidity">
  <div v-if="isInvalidPassword">
    <p>Le mot de passe doit contenir au moins 8 caractères</p>
    <p>Le mot de passe doit contenir au moins un chiffre</p>
    <p>Le mot de passe doit contenir au moins un caractère spécial</p>
  </div>
  <label for="confirm-password"></label>
  <input type="password" v-model="userReInput" @focusout="checkPass" name="confirm-password">
  <p v-if="userInput !== userReInput" class="password-alert">Le mot de passe saisi n'est pas identique</p>
  <button @click="click">Enter the Chest</button>
</template>

<style scoped>
.password-alert {
  color: red;
}
</style>