<template>
  <div class="popupStart">
    <div v-if="!gameStart">
      <div class="container">
        <span>
          {{ Counter }}
        </span>
        <div class="btns">
          <div @click="Up" class="btn-up"><IconChevron /></div>
          <div @click="Down" class="btn-down"><IconChevron /></div>
        </div>
      </div>
      <div @click="Start" class="start">
        <RestartButton :text="text" />
      </div>
    </div>
  </div>
</template>

<script>
import IconChevron from "@/assets/icons/icon-chevron.vue";
import RestartButton from "./Restart-button.vue";

export default {
  props: ["gameStart"],
  components: { IconChevron, RestartButton },
  data() {
    return {
      Counter: 1,
      text: "START",
    };
  },
  methods: {
    Start() {
      this.$emit("Start", this.Counter);
    },
    Up() {
      this.Counter++;
    },
    Down() {
      if (this.Counter > 1) {
        this.Counter--;
      }
    },
  },
};
</script>

<style scoped lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
@mixin hover {
  transition: 200ms;
  border-radius: 10px;
}
@mixin button {
  width: 50px;
  height: 50px;
  transition: 200ms;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  border-top-left-radius: 10px;
  border-top-right-radius: 10px;
}

.seporator {
  height: 2px;
  width: 45px;
  background-color: rgba(0, 0, 0, 0.5);
}
.btns {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.btn-up {
  @include button;

  &:hover {
    background-color: #0000001a;
    cursor: pointer;
  }
}
.btn-down {
  @include button;
  transform: rotate(180deg);
  &:hover {
    background-color: #0000001a;
    cursor: pointer;
  }
}
.popupStart {
  user-select: none;
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
}
.container {
  margin-bottom: 50px;
  display: flex;
  width: 120px;
  height: 100px;
  border-radius: 10px;
  -webkit-backdrop-filter: blur(40px);
  backdrop-filter: blur(40px);
  background-color: rgba(255, 255, 255, 0.5);
  box-shadow: 10px 10px 10px rgb(46 54 68 / 7%);

  align-items: center;
  justify-content: space-between;
  span {
    margin-left: 10px;
  }
}
.start {
  width: 100%;
  display: flex;
  justify-content: center;
}
</style>
