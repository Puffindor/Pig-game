<template>
  <div class="popup">
    <div class="container"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: 1,
    };
  },
};
</script>

<style scoped lang="scss">
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
}
.container {
  transition: 200ms;
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: "Poppins", sans-serif;
  font-weight: 400;
  width: 569px;
  height: 697px;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(40px);
  box-shadow: 10px 10px 10px rgba(46, 54, 68, 0.07);
  border: 2px solid rgba(0, 0, 0, 0.03);
  border-radius: 10px;
}
</style>
