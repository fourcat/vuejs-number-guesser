<script setup>
import { ref } from 'vue';

function getRandomInt(max) {
  return Math.floor(Math.random() * max) + 1;
}

const maximumValue = 100
const number = ref(getRandomInt(maximumValue))

const maxAttempts = 10
const attemptCount = 0

const guess = ref('')

const message = ref('')

function init() {
    number.value = getRandomInt(maximumValue)
    attemptCount.value = 0
}

function check() {
    attemptCount++;
    if (attemptCount >= maxAttempts) {

    }
}
</script>

<template>
    <div>
        <h1>A quel nombre je pense (1 - 100) ?</h1>
        <p>
            <label for="guess">Nombre :</label>
            <input type="number" name="guess" id="guess" v-model="guess">
        </p>
        <p>
            <button type="button" @click="check">Valider</button>
        </p>
        <p>
            {{ message }}
        </p>
    </div>
</template>
