<script setup lang="ts">
import Game from "./components/Game.vue";
</script>

<template>
  <section class="ScoreWrapper">
    <img class="Logo" src="./assets/logo-bonus.svg" alt="logo" />
    <div class="ScoreCard">
      <div class="ScoreCard__Text">SCORE</div>
      <div class="Score">01</div>
    </div>
  </section>
  <section class="GameField">
    <Game />
  </section>
  <button class="PlayButton">PLAY AGAIN</button>
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
.PlayButton {
  padding: 0.5rem 3rem;
  border-radius: 0.25rem;
  background: var(--white);
  color: var(--dark-text);
}
</style>
