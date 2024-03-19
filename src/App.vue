<template>
  <div id="app">
    <h1>Simon says</h1>

    <div class="round-and-start">
      <h2>Round: {{ sequence.length }}</h2>
    </div>
    <div class="game-device">
      <button ref="blue"
        :disabled="!interactive"
        class="game-device__btn top-left-btn"
        @click="check('blue')"></button>
      <button ref="red"
        :disabled="!interactive"
        class="game-device__btn top-right-btn"
        @click="check('red')"></button>
      <button ref="yellow"
        :disabled="!interactive"
        class="game-device__btn bottom-left-btn"
        @click="check('yellow')"></button>
      <button ref="green"
        :disabled="!interactive"
        class="game-device__btn bottom-right-btn"
        @click="check('green')"></button>
    </div>

    <form @submit.prevent
      id="difficultyForm">
      <h3>Сложность:</h3>
      <div>
        <div class="difficulty">
          <input :disabled="active"
            type="radio"
            id="easy"
            name="difficulty"
            value="1500"
            v-model="delay">
          <label for="easy">Легкий</label><br>
        </div>

        <div class="difficulty">
          <input :disabled="active"
            type="radio"
            id="medium"
            name="difficulty"
            value="1000"
            v-model="delay">
          <label for="medium">Средний</label><br>
        </div>

        <div class="difficulty">
          <input :disabled="active"
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
        @click="startGame(true)">Старт</button>
    </form>
    <audio ref="blueSound">
      <source src="./assets/blue.mp3"
        type="audio/mpeg">
    </audio>
    <audio ref="redSound">
      <source src="./assets/red.mp3"
        type="audio/mpeg">
    </audio>
    <audio ref="greenSound">
      <source src="./assets/green.mp3"
        type="audio/mpeg">
    </audio>
    <audio ref="yellowSound">
      <source src="./assets/yellow.mp3"
        type="audio/mpeg">
    </audio>
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
    startGame(reset) {
      if (reset) {
        this.userSequence = []
        this.sequence = []
      }

      this.active = true
      this.interactive = false
      const btnColors = ['red', 'green', 'blue', 'yellow']

      let randomColor = btnColors[Math.floor(Math.random() * 4)];
      this.sequence.push(randomColor);

      for (let i = 0; i < this.sequence.length; i++) {
        const selectedBtn = this.$refs[this.sequence[i]];
        setTimeout(() => {
          selectedBtn.classList.add('active-' + this.sequence[i]);
          this.playSound(this.sequence[i])
          setTimeout(() => {
            selectedBtn.classList.remove('active-' + this.sequence[i]);
          }, this.delay / 2);
        }, this.delay * i);
      }
      setTimeout(() => this.interactive = true, this.delay * this.sequence.length)
      this.userSequence = []
    },
    check(color) {
      this.userSequence.push(color)
      this.playSound(color)
      for (let i = 0; i < this.userSequence.length; i++) {
        if (this.userSequence[i] !== this.sequence[i]) {
          this.active = false
          this.userSequence = []
          this.sequence = []

          this.$refs.blue.classList.remove('active-blue')
          this.$refs.red.classList.remove('active-red')
          this.$refs.yellow.classList.remove('active-yellow')
          this.$refs.green.classList.remove('active-green')
        }
      }
      if (this.active && this.userSequence.length == this.sequence.length)
        setTimeout(() => this.startGame(), 1000)
    },
    playSound(color) {
      const audioElem = this.$refs[color + 'Sound']

      audioElem.currentTime = 0
      audioElem.play()
    }
  },
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
  transition: .1s;
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
.active-blue,
.top-left-btn:hover.active-blue {
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
.active-red,
.top-right-btn:hover.active-red {
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
.active-green,
.bottom-right-btn:hover.active-green {
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
.active-yellow,
.bottom-left-btn:hover.active-yellow {
  background-color: rgb(255, 255, 45);
}
</style>
