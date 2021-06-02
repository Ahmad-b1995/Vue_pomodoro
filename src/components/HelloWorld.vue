<template>
  <div class="hello">
    <div class="card">
      <section :class="`all_cards ${'gone'+focus_setup_page}`">
        <section class="focus_card ">
          <!-- set up focus time -->
          <h1 class="focus_time_title">set up focus time</h1>
          <div class="counter">
            <button class="minus" @click="focus_time--">-</button>
            <h2>{{ focus_time }}</h2>
            <button class="plus" @click="focus_time++">+</button>
          </div>
          <button class="next" @click="focus_setup_page = 2">next</button>
        </section>
        <section class="focus_card">
          <!-- set up focus time -->
          <h1 class="focus_time_title">set up focus time</h1>
          <div class="counter">
            <button class="minus" @click="focus_time--">-</button>
            <h2>{{ focus_time }}</h2>
            <button class="plus" @click="focus_time++">+</button>
          </div>
          <button class="next" @click="focus_setup_page = 3">next</button>
        </section>
        <section class="focus_card">
          <!-- set up focus time -->
          <h1 class="focus_time_title">set up focus time</h1>
          <div class="counter">
            <button class="minus" @click="focus_time--">-</button>
            <h2>{{ focus_time }}</h2>
            <button class="plus" @click="focus_time++">+</button>
          </div>
          <button class="next" @click="focus_setup_page">next</button>
        </section>
      </section>

      <!-- <div>{{ work_time }}</div>
      <input type="text" v-model="work_time" />
      <input type="text" v-model="interval" />
      <button @click="start_pomodoro">start</button> -->
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      focus_time: 25,
      interval: 0,
      focus_setup_page: 1,
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
      const aysncsecond_calculator = this.work_time * 60 * 60;
      this.work_time = aysncsecond_calculator;

      for (var i = 0; i < aysncsecond_calculator; i++) {
        await timeOut(1000);

        this.work_time--;
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

.gone2{
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

.next {
  padding: 0.5rem;
  border-radius: 0.5rem;
  font-size: 0.98rem;
  font-weight: 400;
}
</style>
