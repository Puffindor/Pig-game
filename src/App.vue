<template>
  <div class="con">
    <Winpopup @Restart="Restart" :draw="draw" :win="winner" v-if="gameEnd" />
    <Startpopup
      @Start="Start"
      ref="start"
      :gameStart="gameStart"
      v-if="!gameStart"
    />
    <div class="conatiner">
      <Player1
        ref="p1"
        @PlayerRoll="PlayerRoll"
        @PlayerHold="PlayerHold"
        :roll="Roll"
        :playerTurn="playerTurn1"
      />
      <Rolling
        :roll="rollPrewiev"
        @restart="Restart"
        :rounds="rounds"
        :maxRounds="maxRounds"
      />
      <Player2
        ref="p2"
        @PlayerRoll="PlayerRoll"
        @PlayerHold="PlayerHold"
        :roll="Roll"
        :playerTurn="playerTurn2"
      />
    </div>
  </div>
</template>

<script>
import Player1 from "./components/Player1.vue";
import Player2 from "./components/Player2.vue";
import Rolling from "./components/Rolling.vue";
import Startpopup from "./components/UI/Startpopup.vue";
import Winpopup from "./components/UI/Winpopup.vue";
export default {
  components: { Player1, Player2, Rolling, Winpopup, Startpopup },
  data() {
    return {
      Roll: 0,
      rollPrewiev: "",
      playerTurn1: true,
      playerTurn2: false,
      gameEnd: false,
      gameStart: false,
      winner: "",
      rounds: 1,
      maxRounds: "",
      draw: false,
      i: 0,
    };
  },
  methods: {
    Sleep() {
      return new Promise((resolve) => setTimeout(resolve, 50));
    },
    Start(el) {
      this.gameStart = true;
      this.maxRounds = el;
    },
    Restart() {
      this.$refs.p1.Restart();
      this.$refs.p2.Restart();
      this.Roll = "";
      this.rounds = 1;
      this.i = 0;
      this.winner = "";
      this.gameEnd = false;
      this.gameStart = false;
      this.draw = false;
    },
    async PlayerRoll() {
      for (let i = 0; i < 20; i++) {
        await this.Sleep();
        this.rollPrewiev = Math.floor(Math.random() * (6 - 1 + 1)) + 1;
      }
      this.Roll = this.rollPrewiev;
      this.$refs.p1.Add(this.Roll);
      this.$refs.p2.Add(this.Roll);
    },
    PlayerHold() {
      this.i++;
      this.playerTurn1 = !this.playerTurn1;
      this.playerTurn2 = !this.playerTurn2;
      if (this.i % 2 === 0) {
        this.rounds++;
      }
      let p1 = this.$refs.p1.totalScore;
      let p2 = this.$refs.p2.totalScore;
      if (this.rounds === this.maxRounds) {
        this.gameEnd = true;
        if (p1 === p2) {
          this.draw = true;
        } else {
          if (p1 > p2) {
            this.winner = "PLAYER 1";
          } else {
            this.winner = "PLAYER 2";
          }
        }
      }
    },
  },
  watch: {
    rounds: function () {},
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.con {
  width: 100vw;
  height: 100vh;
  overflow-x: hidden;
}
.conatiner {
  position: absolute;
  z-index: 2;
  overflow: hidden;
  display: flex;
  width: 100%;
  height: 100vh;
  justify-content: space-around;
  align-items: center;
  padding: 30px;
  backdrop-filter: blur(60px);

  background: linear-gradient(
    317deg,
    rgba(255, 0, 200, 0.5),
    rgba(175, 0, 255, 0.5),
    rgba(0, 219, 255, 0.5)
  );
  background-size: 600% 600%;

  -webkit-animation: AnimationName 36s ease infinite;
  -moz-animation: AnimationName 36s ease infinite;
  animation: AnimationName 36s ease infinite;
  background-size: 600% 600%;
}
@-webkit-keyframes AnimationName {
  0% {
    background-position: 0% 88%;
  }
  50% {
    background-position: 100% 13%;
  }
  100% {
    background-position: 0% 88%;
  }
}
@-moz-keyframes AnimationName {
  0% {
    background-position: 0% 88%;
  }
  50% {
    background-position: 100% 13%;
  }
  100% {
    background-position: 0% 88%;
  }
}
@keyframes AnimationName {
  0% {
    background-position: 0% 88%;
  }
  50% {
    background-position: 100% 13%;
  }
  100% {
    background-position: 0% 88%;
  }
}
</style>
