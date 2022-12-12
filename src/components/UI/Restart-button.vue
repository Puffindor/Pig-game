<template>
  <div class="button">{{ text }}</div>
</template>

<script>
export default {
  props: ["text"],
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins");
.button {
  transition: 200ms;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  color: black;
  font-size: 16px;
  border-style: hidden;
  border-radius: 15px;
  box-shadow: 0px 0px 50px rgba(46, 54, 68, 0.3);
  font-family: "Poppins", sans-serif;
  font-weight: 500;
  display: flex;
  align-items: center;
  width: 100px;
  height: 70px;
  &:hover {
    transition: 200ms;
    height: 70px;
    background-color: rgba(255, 255, 255, 0.518);
    transition: 200ms;
    letter-spacing: 1px;
  }
  &:active {
    transition: 200ms;
    transition: 100ms;
    font-size: 14px;
  }
}
</style>
