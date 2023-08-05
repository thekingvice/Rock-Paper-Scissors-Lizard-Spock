<script setup lang="ts">
import Game from "./components/Game.vue";

import { ref } from "vue";

const ScoreCounter = ref(0);

const RulesIsVisible = ref(false);

function UpdateScore() {
  ScoreCounter.value += 1;
}

function ResetScore() {
  ScoreCounter.value = 0;
}

function HandleRulesVisibility() {
  RulesIsVisible.value = !RulesIsVisible.value;
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
  <button class="Rules" v-on:click="HandleRulesVisibility">RULES</button>
  <div
    class="Rules__DiagramWrapper"
    :style="{
      display: RulesIsVisible ? 'flex' : 'none',
      zIndex: RulesIsVisible ? '1' : '-1',
    }"
  >
    <div class="Rules__Modal">
      <p class="Rules__CloseWrapper">
        RULES
        <img
          src="./assets/icon-close.svg"
          alt="close-rules"
          class="Rules__Close"
          v-on:click="HandleRulesVisibility"
        />
      </p>
      <img
        src="./assets/image-rules-bonus.svg"
        alt="rules"
        class="Rules__Diagram"
      />
    </div>
  </div>
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

.Rules__DiagramWrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.25);
}

.Rules__CloseWrapper {
  display: flex;
  justify-content: space-between;
  padding: 0 1rem;
  width: 100%;
}

.Rules__Modal {
  background: var(--white);
  padding: 1.5rem;
  border-radius: 0.5rem;
  max-width: 25rem;
  width: 100%;
  margin: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  font-size: 2rem;
  color: var(--dark-text);
}

.Rules__Close {
  cursor: pointer;
  width: 1.5rem;
  height: 1.5rem;
  align-self: center;
}
</style>
