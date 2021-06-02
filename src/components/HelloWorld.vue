<template>
  <div class="hello">
    <div class="card">
      <section :class="`all_cards ${'gone' + focus_setup_page}`">
        <section class="focus_card">
          <!-- set up focus time -->
          <h1 class="focus_time_title">set up focus time 🎯</h1>
          <div class="counter">
            <button class="minus" @click="focus_time--">-</button>
            <h2>{{ focus_time }}</h2>
            <button class="plus" @click="focus_time++">+</button>
          </div>
          <button class="next" @click="focus_setup_page = 2">next</button>
        </section>
        <section class="focus_card">
          <!-- set up focus time -->
          <h1 class="focus_time_title">set up break time 💤</h1>
          <div class="counter">
            <button class="minus" @click="break_time--">-</button>
            <h2>{{ break_time }}</h2>
            <button class="plus" @click="break_time++">+</button>
          </div>
          <div>
            <button class="back" @click="focus_setup_page = 1">back</button>
            <button class="next" @click="focus_setup_page = 3">next</button>
          </div>
        </section>
        <section class="focus_card">
          <!-- set up focus time -->

          <h1 class="focus_time_title">
            {{ is_break ? "yay! let's take a break 🎉" : "get to work!! 🏃‍♂️🏃" }}
          </h1>
          <div class="counter">
            <h2>{{ minutes }} : {{ seconds }}</h2>
          </div>
          <button
            :class="!is_started ? 'back' : 'back invisible'"
            @click="
              start_pomodoro();
              is_started = !is_started;
            "
          >
            start
          </button>
        </section>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      focus_time: 25,
      break_time: 5,
      is_started: false,
      interval: 0,
      focus_setup_page: 1,
      minutes: 0,
      seconds: 0,
      is_break: false,
    };
  },
  methods: {
    start_pomodoro: async function () {
      // function with promise
      function timeOut(millisecond) {
        return new Promise((resolve) => {
          setTimeout(() => {
            resolve("");
          }, millisecond);
        });
      }
      this.minutes = this.focus_time - 1;
      this.seconds = 60;

      for (var i = 60; i > -1; i--) {
        await timeOut(1000);
        this.seconds--;
        console.log(i);
        if (this.seconds === -1) {
          this.minutes--;
          this.seconds = 60;
          i = 61;
        }
        if (this.minutes === 0 && this.seconds === 0) break;
      }

      // handling break timer
      this.is_break = true;
      this.minutes = this.break_time - 1;
      this.seconds = 60;

      for (var x = 60; x > -1; x--) {
        await timeOut(1000);
        this.seconds--;
        console.log(x);
        if (this.seconds === -1) {
          this.minutes--;
          this.seconds = 60;
          i = 61;
        }
        if (this.minutes === 0 && this.seconds === 0) break;
      }
    },
  },
};
</script>

<style scoped>
* {
  font-size: 1.8rem;
}

button {
  background-color: transparent;
  border: 2px solid #464646;
  outline: none;
  cursor: pointer;
}
button:hover {
  background-color: #424242;
}

button:active {
  background-color: #1b1b1b;
}

.card {
  padding: 1rem 0;
  position: fixed;
  top: 50%;
  left: 50%;
  aspect-ratio: 10/7;
  max-width: 360px;
  min-width: 360px;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -60%);
  overflow: hidden;
  border: 1px solid #464646;
  background-color: #262626;
  border-radius: 1rem;
}

.all_cards {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  width: 1080px;
  transition: all 900ms ease;
}

.focus_card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  width: 365px;
}

.gone1 {
  transform: translateX(0px);
}
.gone2 {
  transform: translateX(-360px);
}

.gone3 {
  transform: translateX(-720px);
}

.counter {
  display: flex;
  justify-content: center;
  align-items: center;
}

.counter h2 {
  font-size: 3rem;
  margin: 0 1rem;
}

.focus_time_title {
  font-size: 0.98rem;
  font-weight: 400;
}

.plus,
.minus {
  border-radius: 0.8rem;

  width: 2.5rem;
  aspect-ratio: 1/1;
}

.next,
.back {
  padding: 0.5rem;
  margin: 0 0.2rem;
  border-radius: 0.5rem;
  font-size: 0.98rem;
  font-weight: 400;
}

.setting_and_title {
  display: flex;
  align-items: center;
  width: 100%;
  justify-content: space-between;
  padding: 0 1rem;
}

.setting_and_title h1 {
  flex: 1;
}

.setting_icon {
  height: 1rem;
  cursor: pointer;
}

.setting_icon:hover {
  transform: scale(1.2);
}

.invisible {
  visibility: hidden;
}
</style>
