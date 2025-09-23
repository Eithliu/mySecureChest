<script setup lang="ts">
import { LogicalPosition } from "@tauri-apps/api/dpi";
import { ref } from "vue";

const props = defineProps<{
    isGenerator: boolean;
    length: string;
}>();

const numberChosen = ref(false);
const specialCharsChosen = ref(false);
const lowerCaseCharsChosen = ref(false);
const upperCaseCharsChosen = ref(false);
const pickedLength = ref("");

function randomisePassword(length: string): string {
    let result = [];
    let lowerCaseChars = "abcdefghijklmnopqrstuvwxyz";
    let upperCaseChars = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    let numbers = "0123456789";
    let specialChars = 'éèçà!è§(&@-_)#@êëù%$*€`£=+/:.;?,âäûüîïôö"';

    for (let i = 0; i < +length; i++) {
        const setOfChars = lowerCaseChars;
        const randomIndex = getSecureRandomInt(setOfChars.length);
        result.push(setOfChars[randomIndex]);
        if (numberChosen.value) {
            const setOfChars = lowerCaseChars + numbers;
            const randomIndex = getSecureRandomInt(setOfChars.length);

            result.push(setOfChars[randomIndex]);
        } else if (specialCharsChosen.value) {
            const setOfChars = lowerCaseChars + specialChars;
            const randomIndex = getSecureRandomInt(setOfChars.length);

            result.push(setOfChars[randomIndex]);
        } else if (numberChosen.value && specialCharsChosen.value) {
            const setOfChars = lowerCaseChars + numbers + specialChars;
            const randomIndex = getSecureRandomInt(setOfChars.length);

            result.push(setOfChars[randomIndex]);
        }
    }
    return result.join("");
}

function getSecureRandomInt(max: number): number {
    // Utilise l'API Web Crypto pour une génération cryptographiquement sécurisée
    const array = new Uint32Array(1);
    crypto.getRandomValues(array);

    // Évite le biais modulo avec rejection sampling
    const maxValidValue = Math.floor(0xffffffff / max) * max;
    let randomValue = array[0];

    while (randomValue >= maxValidValue) {
        crypto.getRandomValues(array);
        randomValue = array[0];
    }

    return randomValue % max;
}

function displayGeneratedPassword(length: string) {
    return randomisePassword(length);
}
</script>

<template>
    <div class="what-to-include">
        <p>Include</p>
        <div class="can-include">
            <div>
                <label for="characters">lower-case characters</label>
                <input
                    type="checkbox"
                    value="Characters"
                    id="characters"
                    v-model="lowerCaseCharsChosen"
                />
            </div>
            <div>
                <label for="upperCaseCharacters">upper-case characters</label>
                <input
                    type="checkbox"
                    value="upperCaseCharacters"
                    id="upperCaseCharacters"
                    v-model="upperCaseCharsChosen"
                />
            </div>
            <div>
                <label for="numbers">numbers</label>
                <input
                    type="checkbox"
                    value="Numbers"
                    id="numbers"
                    v-model="numberChosen"
                />
            </div>
            <div>
                <label for="special-chars">special characters</label>
                <input
                    type="checkbox"
                    value="Special characters"
                    id="special-chars"
                    v-model="specialCharsChosen"
                />
            </div>
        </div>
    </div>
    <p>Value must be between 8 and 128</p>
    <label for="length">Length</label>
    <input
        type="number"
        v-model="pickedLength"
        id="length"
        name="length"
        placeholder="8"
    />
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
