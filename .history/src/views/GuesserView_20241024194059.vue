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
    <main class="form-signin w-100 m-auto">
        <h1>A quel nombre je pense (1 - 100) ?</h1>
        <div class="form-floating">
            <input class="form-control" type="number" name="guess" id="guess"
                v-model="guess"
                @keyup.enter="check"
                placeholder="Nombre">
        </div>
    </main>
    <div class="d-flex flex-column flex-md-row p-4 gap-4 py-md-5 align-items-center justify-content-center">
        <div class="list-group">
            <div class="list-group-item list-group-item-action d-flex gap-3 py-3">
                <h1>A quel nombre je pense (1 - 100) ?</h1>
            </div>
            <div class="list-group-item list-group-item-action d-flex gap-3 py-3">
                <label for="guess">Nombre :</label>
                <input type="number" name="guess" id="guess" v-model="guess" @keyup.enter="check">
            </div>
            <div class="d-flex gap-2 justify-content-center py-5">
                <button
                    class="btn btn-primary d-inline-flex align-items-center"
                    type="button"
                    v-if="maxAttemptsReached || guessed" disabled>
                        Valider
                </button>
                <button
                    class="btn btn-primary d-inline-flex align-items-center"
                    type="button"
                    v-else @click="check">
                        Valider
                </button>
                <button
                    class="btn btn-primary d-inline-flex align-items-center"
                    type="button"
                    @click="reset">
                        Un autre !
                </button>
            </div>
            <div class="list-group-item list-group-item-action d-flex gap-3 py-3">
                <b>{{ message }}</b>
            </div>
        </div>
    </div>
</template>
