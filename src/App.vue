<script setup lang="ts">
import Game from "./components/Game.vue";

import { ref } from "vue";

const ScoreCounter = ref(0);

function UpdateScore() {
  ScoreCounter.value += 1;
}

function ResetScore() {
  ScoreCounter.value = 0;
}
</script>

<template>
  <section class="ScoreWrapper">
    <img
      class="Logo"
      v-on:click="UpdateScore"
      src="./assets/logo-bonus.svg"
      alt="logo"
    />
    <div class="ScoreCard">
      <div class="ScoreCard__Text">SCORE</div>
      <div class="Score">{{ ScoreCounter }}</div>
    </div>
  </section>
  <section class="GameField">
    <Game
      :ScoreCounter.sync="ScoreCounter"
      @UpdateScore="UpdateScore"
      @ResetScore="ResetScore"
    />
  </section>
  <button class="Rules">RULES</button>
</template>

<style scoped>
.ScoreWrapper {
  display: flex;
  justify-content: space-between;
  max-width: 100%;
  width: 20rem;
  border: 3px solid hsl(217, 16%, 45%);
  border-radius: 0.5rem;
  padding: 1rem;
}
.ScoreCard {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  padding: 1rem 2rem;
  border-radius: 0.5rem;
  background: var(--white);
}
.ScoreCard__Text {
  color: var(--score-text);
}

.Score {
  font-size: 2rem;
}
.Logo {
  width: 7rem;
}

.GameField {
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.Rules {
  color: var(--white);
  border: 2px solid hsl(217, 16%, 45%);
  padding: 0.5rem 2rem;
  border-radius: 0.5rem;
  cursor: pointer;
}

.Rules:hover {
  background: var(--white);
  color: var(--dark-text);
}
</style>
