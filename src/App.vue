<template>
  <div id="app">
    <h1>Simon says</h1>

    <div class="round-and-start">
      <h2>Round: {{ sequence.length }}</h2>
    </div>
    <div class="game-device">
      <button ref="blue"
        class="game-device__btn top-left-btn"
        @click="check"></button>
      <button ref="red"
        class="game-device__btn top-right-btn"
        @click="check"></button>
      <button ref="yellow"
        class="game-device__btn bottom-left-btn"
        @click="check"></button>
      <button ref="green"
        class="game-device__btn bottom-right-btn"
        @click="check"></button>
    </div>

    <form @submit.prevent
      id="difficultyForm">
      <h3>Сложность:</h3>
      <div>
        <div class="difficulty">
          <input :disabled="!interactive"
            type="radio"
            id="easy"
            name="difficulty"
            value="1500"
            v-model="delay">
          <label for="easy">Легкий</label><br>
        </div>

        <div class="difficulty">
          <input :disabled="!interactive"
            type="radio"
            id="medium"
            name="difficulty"
            value="1000"
            v-model="delay">
          <label for="medium">Средний</label><br>
        </div>

        <div class="difficulty">
          <input :disabled="!interactive"
            type="radio"
            id="hard"
            name="difficulty"
            value="400"
            v-model="delay">
          <label for="hard">Сложный</label><br>
        </div>
      </div>
      <button :disabled="!interactive"
        class="start-btn"
        @click="startGame()">Старт</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      sequence: [],
      userSequence: [],
      delay: 1500,
      interactive: true,
      active: false,
    }
  },
  methods: {
    startGame() {
      this.active = true
      this.interactive = false
      const btnColors = ['red', 'green', 'blue', 'yellow'],
        randomColor = btnColors[Math.floor(Math.random() * 4)]

      this.sequence.push(randomColor)

      const selectedBtn = this.$refs[randomColor]
      setInterval(() => {

        selectedBtn.classList.add('active-' + randomColor)

        setTimeout(() => {
          selectedBtn.classList.remove('active-' + randomColor)
        }, this.delay);

      }, this.delay);

      this.interactive = true
    },
    check() {
      for (let i = 0; i < this.userSequence.length; i++) {
        console.log(this.userSequence[i] !== this.sequence[i])
        if (this.userSequence[i] !== this.sequence[i]) this.active = false
        else this.startGame()
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 1rem;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  align-items: center;
}


#difficultyForm {
  display: flex;
  align-items: center;
}

.difficulty + .difficulty {
  margin-top: 0.5rem;
}

.start-btn {
  background-color: rgb(59, 238, 238);
  border: 0;
  padding: 0.5rem 2rem;
  height: 3rem;
  font-weight: bold;
  font-size: x-large;
  margin-left: 3rem;
  border-radius: 1rem;
  color: #2c3e50;
  transition: .2s;
}

.start-btn:hover {
  background-color: rgb(0, 148, 148);
}

.start-btn:active {
  background-color: aqua;
}


.game-device {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-content: space-between;
  width: 18rem;
  height: 18rem;
  background-color: white;
  border-radius: 50%;
  padding: 0.5rem;
  box-shadow: 0px 0px 10px black;
  margin-top: 2rem;
  margin-bottom: 3rem;
}

.game-device__btn {
  width: 50%;
  height: 50%;
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

.top-left-btn:active,
.active-blue {
  background-color: rgb(0, 191, 255);
}


.top-right-btn {
  border-top-right-radius: 100%;
  background-color: rgb(218, 106, 106);
}

.top-right-btn:hover {
  background-color: rgb(150, 59, 59);
}

.top-right-btn:active,
.active-red {
  background-color: rgb(255, 0, 0);
}

.bottom-right-btn {
  border-bottom-right-radius: 100%;
  background-color: rgb(101, 218, 101);
}

.bottom-right-btn:hover {
  background-color: rgb(54, 124, 54);
}

.bottom-right-btn:active,
.active-green {
  background-color: rgb(41, 228, 41);
}


.bottom-left-btn {
  border-bottom-left-radius: 100%;
  background-color: rgb(224, 224, 112);
}

.bottom-left-btn:hover {
  background-color: rgb(194, 194, 61);
}

.bottom-left-btn:active,
.active-yellow {
  background-color: rgb(255, 255, 45);
}
</style>
