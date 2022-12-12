<template>
  <div
    :class="{ 'player-active': playerTurn, 'player-passive': !playerTurn }"
    style="backdrop-filter: blur(20px)"
  >
    <div class="scores">
      <span class="player-string">PLAYER 2</span>
      <span class="total-score"
        >TOTAL SCORE<br />
        {{ this.totalScore }}</span
      >
      <span class="score"
        >Mach score<br />
        {{ this.machScore }}</span
      >
      <DoubleButton @hold="Hold" @reroll="Roll" />
    </div>
  </div>
</template>

<script>
import DoubleButton from "./UI/Double-button.vue";

export default {
  props: ["roll", "playerTurn"],
  data() {
    return {
      totalScore: 0,
      machScore: 0,
    };
  },
  methods: {
    Restart() {
      this.totalScore = 0;
      this.machScore = 0;
    },
    Roll() {
      console.log(12323);
      if (this.playerTurn == true) {
        this.$emit("PlayerRoll");
      }
    },
    Hold() {
      if (this.playerTurn == true) {
        this.totalScore = this.totalScore + this.machScore;
        this.machScore = 0;
        this.$emit("PlayerHold");
      }
    },
    Add(el) {
      if (this.playerTurn == true) {
        this.machScore = this.machScore + Number(el);
        if (el === 1) {
          console.log(el);
          this.machScore = 0;
          this.$emit("PlayerHold");
        }
      }
    },
  },
  computed: {
    Turn() {
      if (this.playerTurn) {
        return "#6e3a81";
      } else {
        return "rgba(110, 58, 129, 0.5)";
      }
    },
  },
  components: { DoubleButton },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins");

@mixin player {
  transition: 200ms;
  user-select: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Poppins", sans-serif;
  font-weight: 400;
  width: 30%;
  height: 80%;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(40px);
  box-shadow: 10px 10px 10px rgba(46, 54, 68, 0.07);
  border: 2px solid rgba(0, 0, 0, 0.03);
  border-radius: 10px;
}
.player-string {
  color: rgba(220, 49, 60, 1);
  text-shadow: 0 0 18px rgba(220, 49, 60, 1);
  font-size: 20px;
  font-weight: 800;
}
.player-active {
  transform: scale(1.05);
  @include player();
}
.player-passive {
  transform: scale(0.9);
  @include player();
}

.scores {
  display: flex;
  height: 100%;
  width: 100%;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}
.total-score {
  display: flex;
  text-align: center;
  flex-direction: column;
  color: rgb(255, 255, 255);
  text-shadow: 0 0 10px rgb(208, 210, 248);
  font-size: 60px;
  width: 200%;
}

.score {
  font-size: 40px;
  color: white;
  width: 100%;
  display: flex;
  justify-items: center;
  align-items: center;
  flex-direction: column;
  text-align: center;
  color: rgb(255, 255, 255);
  text-shadow: 0 0 10px rgb(208, 210, 248);
}
@media screen and (max-width: 1400px) {
  .total-score {
    font-size: 40px;
  }
  .score {
    font-size: 30px;
  }
}
</style>
