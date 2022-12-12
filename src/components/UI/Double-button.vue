<template>
  <div class="btns">
    <div class="btn-hold" @click="Hold">HOLD</div>
    <div class="seporator"></div>
    <div class="btn-rerol" @click="Reroll">REROL</div>
  </div>
</template>

<script>
export default {
  methods: {
    Hold() {
      this.$emit("hold");
    },
    Reroll() {
      this.$emit("reroll");
    },
  },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins");

@mixin btn {
  cursor: pointer;

  display: flex;
  align-items: center;
  justify-content: center;
  width: 100px;
  height: 70px;
  background-color: white;
  transition: 200ms;
}
.btns {
  border-style: hidden;
  border-radius: 15px;
  box-shadow: 0px 0px 50px rgba(46, 54, 68, 0.3);
  font-family: "Poppins", sans-serif;
  font-weight: 500;
  display: flex;
  align-items: center;
  .btn-hold {
    @include btn;
    transform: translateX(1px);
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;

    &:hover {
      height: 70px;
      background-color: rgba(255, 255, 255, 0.518);
      transition: 200ms;
      letter-spacing: 1px;
    }
    &:active {
      transition: 100ms;
      font-size: 14px;
    }
  }
  .btn-rerol {
    @include btn;
    transform: translateX(-1px);
    border-top-right-radius: 15px;
    border-bottom-right-radius: 15px;
    &:hover {
      height: 70px;
      background-color: rgba(255, 255, 255, 0.518);
      transition: 200ms;
      letter-spacing: 1px;
    }
    &:active {
      transition: 100ms;
      font-size: 14px;
    }
  }
}

.seporator {
  z-index: 10;
  width: 2px;
  height: 80%;
  background-color: rgb(198, 196, 196);
}
</style>
