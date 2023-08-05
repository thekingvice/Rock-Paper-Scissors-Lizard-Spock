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
          src="/images/icon-scissors.svg"
          alt="scissors"
        /></button
      ><button
        class="Game__OptionButton Paper"
        v-on:click="HandlePick('Paper')"
      >
        <img
          class="Game__OptionButtonIcon"
          src="/images/icon-paper.svg"
          alt="paper"
        /></button
      ><button class="Game__OptionButton Rock" v-on:click="HandlePick('Rock')">
        <img
          class="Game__OptionButtonIcon"
          src="/images/icon-rock.svg"
          alt="rock"
        /></button
      ><button
        class="Game__OptionButton Lizard"
        v-on:click="HandlePick('Lizard')"
      >
        <img
          class="Game__OptionButtonIcon"
          src="/images/icon-lizard.svg"
          alt="lizard"
        /></button
      ><button
        class="Game__OptionButton Spock"
        v-on:click="HandlePick('Spock')"
      >
        <img
          class="Game__OptionButtonIcon"
          src="/images/icon-spock.svg"
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
      <div class="Game__PicksWrapper Game__You">
        <p>YOU PICKED</p>
        <button
          class="Game__Picks"
          :style="{ borderColor: OptionData[Player1].Color }"
        >
          <img
            class="Game__OptionButtonIcon"
            :src="OptionData[Player1].src"
            alt="you"
          />
        </button>
      </div>

      <div class="Game__ResultWrapper">
        <h1>{{ Result }}</h1>
        <button class="Game__PlayButton" v-on:click="HandlePlayAgain">
          PLAY AGAIN
        </button>
      </div>
      <div class="Game__PicksWrapper Game__House">
        <p>HOUSE PICKED</p>
        <button
          class="Game__Picks"
          :style="{ borderColor: OptionData[Player2].Color }"
        >
          <img
            class="Game__OptionButtonIcon"
            :src="OptionData[Player2].src"
            alt="opponent"
          />
        </button>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref } from "vue";

const IsVisible = ref(true);

// const props: any = defineProps({ ScoreCounter: Number });

const emits = defineEmits(["UpdateScore", "ResetScore"]);

const Player1 = ref("Rock");

const Player2 = ref("Paper");

const IsLoss = ref(false);

const Result = ref("");

type OptionData = {
  [key: string]: {
    src: string;
    Color: string;
  };
};

const OptionData: OptionData = {
  Rock: {
    src: "/images/icon-rock.svg",
    Color: "hsl(349, 71%, 52%)",
  },
  Paper: {
    src: "/images/icon-paper.svg",
    Color: "hsl(230, 89%, 62%)",
  },
  Scissors: {
    src: "/images/icon-scissors.svg",
    Color: "hsl(39, 89%, 49%)",
  },
  Lizard: {
    src: "/images/icon-lizard.svg",
    Color: "hsl(261, 73%, 60%)",
  },
  Spock: {
    src: "/images/icon-spock.svg",
    Color: "hsl(189, 59%, 53%)",
  },
};

function HandlePlayAgain() {
  if (IsLoss.value) {
    IsLoss.value = !IsLoss.value;
    emits("ResetScore");
  }
  IsVisible.value = !IsVisible.value;
}

function HandlePick(Option: string) {
  Player1.value = Option;
  FindWinner(Player1.value);
}

function FindWinner(P1: string) {
  const Options = ["Rock", "Paper", "Scissors", "Lizard", "Spock"];

  type WinningOptions = {
    [key: string]: string[];
  };

  const Winning: WinningOptions = {
    Rock: ["Scissors", "Lizard"],
    Paper: ["Rock", "Spock"],
    Scissors: ["Lizard", "Paper"],
    Lizard: ["Paper", "Spock"],
    Spock: ["Rock", "Scissors"],
  };

  let P2 = Options[Math.floor(Math.random() * 5)];

  Player2.value = P2;

  if (P1 === P2) {
    Result.value = "TIE.";
  } else if (Winning[P1].includes(P2)) {
    Result.value = "YOU WIN!";
    emits("UpdateScore");
  } else {
    Result.value = "YOU LOSE.";
    IsLoss.value = true;
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
  transition: all 0.5s;
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
  cursor: pointer;
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
  gap: 1rem;
  transition: all 0.5s;
  align-items: center;
  justify-content: space-between;
  display: grid;
  grid-template-columns: repeat(3, 7rem);
}

.Game__ResultWrapper {
  display: flex;
  flex-direction: column;
  color: var(--white);
  font-size: 2rem;
  align-items: center;
  gap: 1rem;
  white-space: nowrap;
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

.Game__PicksWrapper {
  display: flex;
  flex-direction: column;
  color: var(--white);
  align-items: center;
  gap: 1rem;
  white-space: nowrap;
}

.Game__PlayButton {
  font-size: 1rem;
  background: var(--white);
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  cursor: pointer;
  color: var(--dark-text);
}

.Game__PlayButton:hover {
  box-shadow: -0px 0px 5px 3px rgba(255, 255, 255, 0.5);
}

@media only screen and (max-width: 600px) {
  .Game {
    --percentage: 0.5rem;
  }

  .Game__OptionButton {
    width: 5rem;
    height: 5rem;
    border: 0.5rem solid;
  }
  .Scissors {
    border-color: hsl(39, 89%, 49%);
  }
  .Paper {
    border-color: hsl(230, 89%, 62%);
  }
  .Rock {
    border-color: hsl(349, 71%, 52%);
  }

  .Lizard {
    border-color: hsl(261, 73%, 60%);
  }

  .Spock {
    border-color: hsl(189, 59%, 53%);
  }

  .Game__OptionButtonIcon {
    width: 1.5rem;
  }

  .Game__Picks {
    width: 5rem;
    height: 5rem;
    border: 0.5rem solid;
  }

  .Game__Results {
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
  }

  .Game__ResultWrapper {
    grid-column: 1 / span 2;
  }

  .Game__You {
    grid-column: 1;
    grid-row: 1;
  }

  .Game__House {
    grid-column: 2;
    grid-row: 1;
  }

  .Game__Wrapper {
    top: 5rem;
  }
}
</style>
