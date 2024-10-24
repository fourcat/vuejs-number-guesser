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
    return attemptCount.value >= maxAttempts;
})

const guess = ref('')
const guessed = ref(false)

const message = ref('')

function reset() {
    number.value = getRandomInt(maximumValue);
    attemptCount.value = 0;
    guess.value = '';
    guessed.value = false;
    message.value = '';
}

function check() {
    attemptCount.value++;
    console.log('attemptCount.value : ' + attemptCount.value);
    if (maxAttemptsReached.value) {
        message.value = "Vous avez atteint le nombre d'essais max.";
    } else if (parseInt(guess.value) == number.value) {
        message.value = "Vous avez trouvé !";
        guessed.value = true;
    } else if (parseInt(guess.value) < number.value) {
        message.value = "Trop petit";
    } else if (parseInt(guess.value) > number.value) {
        message.value = "Trop grand";
    } else {
        message.value = "Trou noir";
    }
}
</script>

<template>
    <div>
        <h1>A quel nombre je pense (1 - 100) ?</h1>
        <p>
            <label for="guess">Nombre :</label>
            <input type="number" name="guess" id="guess" v-model="guess" @keyup.enter="check">
        </p>
        <p>
            <button type="button" v-if="maxAttemptsReached || guessed" disabled>Valider</button>
            <button type="button" v-else @click="check">Valider</button>
            <button type="button" @click="reset">Un autre !</button>
        </p>
        <p>
            <b>{{ message }}</b>
        </p>
    </div>
</template>
