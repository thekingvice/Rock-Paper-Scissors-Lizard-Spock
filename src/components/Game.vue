<template>
  <div class="Game">
    <div
      class="Game__Wrapper"
      v-on:click="
        () => {
          IsVisible = !IsVisible;
        }
      "
      :style="{
        opacity: IsVisible ? '100%' : '0%',
        visibility: IsVisible ? 'visible' : 'hidden',
      }"
    >
      <button
        class="Game__OptionButton Scissors"
        v-on:click="HandlePick('Scissors')"
      >
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
    <div
      class="Game__Results"
      :style="{
        opacity: IsVisible ? '0%' : '100%',
        visibility: IsVisible ? 'hidden' : 'visible',
      }"
    >
      <button
        class="Game__Picks"
        :style="{ borderColor: OptionData.Rock.Color }"
      >
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-scissors.svg"
          alt="you"
        />
      </button>
      <button class="Game__Picks">
        <img
          class="Game__OptionButtonIcon"
          src="../assets/icon-scissors.svg"
          alt="opponent"
        />
      </button>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";

const IsVisible = ref(true);

const Player1 = ref("");

const Player2 = ref("");

const OptionData = {
  Rock: {
    Name: "Rock",
    src: "../assets/icon-rock.svg",
    Color: "hsl(349, 71%, 52%)",
  },
  Paper: {
    Name: "Paper",
    src: "../assets/icon-paper.svg",
    Color: "hsl(349, 71%, 52%)",
  },
  Scissors: {
    Name: "Scissors",
    src: "../assets/icon-scissors.svg",
    Color: "hsl(349, 71%, 52%)",
  },
  Lizard: {
    Name: "Lizard",
    src: "../assets/icon-lizard.svg",
    Color: "hsl(349, 71%, 52%)",
  },
  Spock: {
    Name: "Spock",
    src: "../assets/icon-spock.svg",
    Color: "hsl(349, 71%, 52%)",
  },
};

function HandlePick(Option: string) {
  Player1.value = Option;
  FindWinner(Player1.value);
}

function FindWinner(P1: string) {
  const Options = ["Rock", "Paper", "Scissors", "Lizard", "Spock"];

  const Winning = {
    Rock: ["Scissors", "Lizard"],
    Paper: ["Rock", "Spock"],
    Scissors: ["Lizard", "Paper"],
    Lizard: ["Paper", "Spock"],
    Spock: ["Rock", "Scissors"],
  };

  let P2 = Options[Math.floor(Math.random() * 5)];

  Player2.value = P2;

  console.log(`You: ${P1}, Opponent: ${P2}`);

  if (P1 === P2) {
    console.log("It's a Tie!");
  } else if (Winning[P1].includes(P2)) {
    console.log("You Win!");
  } else {
    console.log("You Lose...");
  }
}
</script>
<style scoped>
.Game {
  --percentage: 0.75rem;
}

.Game__Wrapper {
  position: relative;
  display: flex;
  justify-content: center;
  transition: all 2s;
}
.Game__OptionButton {
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

.Game__Results {
  display: flex;
  gap: 2rem;
  transition: all 2s;
}

.Game__Picks {
  color: var(--white);
  width: 7rem;
  height: 7rem;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 5rem;
  background: var(--white);
  border: 0.75rem solid grey;
}
</style>
