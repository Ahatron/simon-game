<template>
  <div id="app">
    <div class="game-device">
      <button class="game-device__btn top-left-btn"
        style=""></button>
      <button class="game-device__btn top-right-btn"
        style=""></button>

      <button class="game-device__btn bottom-left-btn"
        style=""></button>
      <button class="game-device__btn bottom-right-btn"
        style=""></button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  box-sizing: border-box;
}

.game-device {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-content: space-between;
  width: 20rem;
  height: 20rem;
  background-color: white;
  border-radius: 50%;
  padding: 1rem;
  box-shadow: 0px 0px 10px black;
}

.game-device__btn {
  width: 49%;
  height: 49%;
  padding: 0;
  border: none;
  transition: .2s;
}

.top-left-btn {
  border-top-left-radius: 100%;
  background-color: rgb(113, 181, 204);
}

.top-left-btn:hover {
  background-color: rgb(0, 103, 138);
}

.top-left-btn:active {
  background-color: rgb(0, 191, 255);
}


.top-right-btn {
  border-top-right-radius: 100%;
  background-color: rgb(218, 106, 106);
}

.top-right-btn:hover {
  background-color: rgb(150, 59, 59);
}

.top-right-btn:active {
  background-color: rgb(255, 0, 0);
}

.bottom-right-btn {
  border-bottom-right-radius: 100%;
  background-color: rgb(101, 218, 101);
}

.bottom-right-btn:hover {
  background-color: rgb(33, 139, 33);
}

.bottom-right-btn:active {
  background-color: rgb(41, 228, 41);
}


.bottom-left-btn {
  border-bottom-left-radius: 100%;
  background-color: rgb(224, 224, 112);
}

.bottom-left-btn:hover {
  background-color: rgb(194, 194, 61);
}

.bottom-left-btn:active {
  background-color: rgb(255, 255, 45);
}
</style>
