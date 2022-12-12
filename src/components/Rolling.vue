<template>
  <div class="rolling">
    <span>ROLL</span>
    <span>{{ rounds }} / {{ maxRounds }}</span>
    <span class="roll" v-if="roll">{{ roll }}</span>
    <span v-if="!roll">0</span>
    <div @click="Restart">
      <RestartButton :text="text" />
    </div>
  </div>
</template>

<script>
import RestartButton from "./UI/Restart-button.vue";

export default {
  data() {
    return {
      text: "RESTART",
    };
  },
  props: ["roll", "rounds", "maxRounds"],
  methods: {
    Restart() {
      this.$emit("restart");
      console.log(this.roll);
    },
  },
  computed: {
    Color() {
      if (this.roll === 1) {
        return "rgba(220, 49, 60, 1)";
      } else return "white";
    },
  },
  components: { RestartButton },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins");
.roll {
  color: v-bind(Color);
}
.rolling {
  user-select: none;
  font-family: "Poppins", sans-serif;
  font-weight: 400;
  color: white;
  font-size: 50px;
  padding: 20px;
  padding-bottom: 50px;
  display: flex;
  width: 18%;
  height: 80%;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(20px);
  box-shadow: 10px 10px 10px rgba(46, 54, 68, 0.07);
  border: 2px solid rgba(46, 54, 68, 0.03);
  border-radius: 10px;
  align-items: center;
  flex-direction: column;
  justify-content: space-between;
}

@media screen and (max-width: 1400px) {
  .rolling {
    font-size: 40px;
  }
}
</style>
