<script setup>
import { computed, ref } from 'vue';

function getRandomInt(max) {
  return Math.floor(Math.random() * max) + 1;
}

const maximumValue = 100
const number = ref(getRandomInt(maximumValue))

const maxAttempts = 10
const attemptCount = ref(0)
const maxAttemptsReached = computed(() => {
    console.log('attemptCount : ' + attemptCount);
    console.log('attemptCount.value >= maxAttempts : ' + attemptCount.value >= maxAttempts);
    return attemptCount.value >= maxAttempts;
})

const guess = ref('')

const message = ref('')

function reset() {
    number.value = getRandomInt(maximumValue);
    attemptCount.value = 0;
    message.value = '';
}

function check() {
    attemptCount.value++;
    console.log('attemptCount.value : ' + attemptCount.value);
    if (maxAttemptsReached.value) {
        message.value = "Vous avez atteint le nombre d'essais max.";
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
            <button type="button" v-if="maxAttemptsReached" disabled>Valider</button>
            <button type="button" v-else @click="check">Valider</button>
            <button type="button" @click="reset">Un autre !</button>
        </p>
        <p>
            <b>{{ message }}</b>
        </p>
    </div>
</template>
