<template>
  <div class="popup">
    <div v-if="!draw">
      <span :class="Winner">{{ win }}</span
      ><br />
      WINS
    </div>
    <div v-if="draw">DRAW</div>
    <div @click="Restart" class="btn-container">
      <RestartButton :text="text" />
    </div>
  </div>
</template>

<script>
import RestartButton from "./Restart-button.vue";

export default {
  data() {
    return {
      text: "RESTART",
    };
  },
  props: ["win", "draw"],
  methods: {
    Restart() {
      this.$emit("Restart", "draw");
    },
  },
  computed: {
    Winner() {
      switch (this.win) {
        case "PLAYER 1":
          return "p1";
        case "PLAYER 2":
          return "p2";
      }
    },
  },
  components: { RestartButton },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins");
.popup {
  flex-direction: column;
  font-family: "Poppins", sans-serif;
  font-weight: 900;
  font-size: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 100;
  width: 100%;
  height: 100%;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  .p1 {
    color: rgba(40, 109, 243, 1);
    text-shadow: 0 0 18px rgba(40, 109, 243, 1);
    font-size: 50px;
    font-weight: 800;
  }
  .p2 {
    color: rgba(220, 49, 60, 1);
    text-shadow: 0 0 18px rgba(220, 49, 60, 1);
    font-size: 50px;
    font-weight: 800;
  }
}
.btn-container {
  margin-top: 20px;
}
</style>
