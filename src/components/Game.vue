<template>
  <div class="Game">
    <div class="Game__Wrapper">
      <button class="Game__OptionButton Scissors">
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-scissors.svg"
          alt="scissors"
        /></button
      ><button class="Game__OptionButton Paper">
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-paper.svg"
          alt="paper"
        /></button
      ><button class="Game__OptionButton Rock">
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-rock.svg"
          alt="rock"
        /></button
      ><button class="Game__OptionButton Lizard">
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-lizard.svg"
          alt=""
        /></button
      ><button class="Game__OptionButton Spock">
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-spock.svg"
          alt="spock"
        />
      </button>
    </div>
  </div>
</template>
<script setup lang="ts"></script>
<style scoped>
.Game {
  --percentage: 0.75rem;
}

.Game__Wrapper {
  position: relative;
  display: flex;
  justify-content: center;
}
.Game__OptionButton {
  font-size: 2rem;
  color: var(--white);
  position: absolute;
  width: 7rem;
  height: 7rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5rem;
  background: var(--white);
  border: 0.75rem solid grey;
}

.Game__OptionButtonIcon {
  width: 2.5rem;
}

.Scissors {
  transform: translate(0, calc(-10 * var(--percentage)));
  border-color: hsl(39, 89%, 49%);
}
.Paper {
  transform: translate(
    calc(9.511 * var(--percentage)),
    calc(-3.09 * var(--percentage))
  );
  border-color: hsl(230, 89%, 62%);
}
.Rock {
  transform: translate(
    calc(5.878 * var(--percentage)),
    calc(8.09 * var(--percentage))
  );
  border-color: hsl(349, 71%, 52%);
}

.Lizard {
  transform: translate(
    calc(-5.878 * var(--percentage)),
    calc(8.09 * var(--percentage))
  );
  border-color: hsl(261, 73%, 60%);
}

.Spock {
  transform: translate(
    calc(-9.511 * var(--percentage)),
    calc(-3.09 * var(--percentage))
  );
  border-color: hsl(189, 59%, 53%);
}
</style>
