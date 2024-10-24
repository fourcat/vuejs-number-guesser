<script setup>
import { ref } from 'vue';

function getRandomInt(max) {
  return Math.floor(Math.random() * max) + 1;
}

const maximumValue = 100
const number = ref(getRandomInt(maximumValue))

const maxAttempts = 10
const attemptCount = ref(0)

const guess = ref('')

function init() {
    number.value = getRandomInt(maximumValue)
    attemptCount.value = 0
}

function check() {
    
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
    </div>
</template>
