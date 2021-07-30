<template>
  <div class="main">
    <div class="main__alarm">{{ minutes }}:{{ remSeconds }}</div>
    <div class="main__buttons">
      <button class="main__button" @click="start">Start</button>
      <button class="main__button" @click="stop">Stop</button>
      <button class="main__button" @click="reset">Reset</button>
    </div>
  </div>
  <!--<div class="content">
    <HeaderComponent />
    <h1>Main Component</h1>
    <router-view />
    <FooterComponent />
  </div>-->
</template>

<script>
import { ref } from "vue";
import HeaderComponent from "./components/shared/Header.vue";
import FooterComponent from "./components/shared/Footer.vue";
export default {
  components: { HeaderComponent, FooterComponent },
  setup() {
    let seconds = 60;
    let minutes = ref(1), remSeconds = ref(0);
    let start, stop, reset;
    let time;
    (minutes.value < 10) ? minutes.value = "0" + minutes.value : minutes.value;
    (remSeconds.value < 10) ? remSeconds.value = "0" + remSeconds.value : remSeconds.value;

    start = () => {
      seconds == 0 ? seconds = 60 : seconds;
      time = setInterval( () => {
        secondspass();
      }, 1000);
    }

    stop = () => {
      clearInterval(time);
    }

    reset = () => {
      seconds = 60;
      secondspass();
      stop();
    }

    function secondspass(){
      minutes.value = Math.floor(seconds / 60);
      remSeconds.value = seconds % 60;
      (minutes.value < 10) ? minutes.value = "0" + minutes.value : minutes.value;
      (remSeconds.value < 10) ? remSeconds.value = "0" + remSeconds.value : remSeconds.value;
      if(seconds > 0){
        seconds--;
      } else {
        clearInterval(time);
      }
    }

    
    
    return {
      minutes,
      remSeconds,
      start,
      stop,
      reset,
    };
  },
};
</script>

<style lang="scss">
.main{
  display: flex;
  flex-direction: column;
  align-items: stretch;
  justify-content: center;
  &__alarm {
    font-size: 20vw;
  }
  &__buttons {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-evenly;
  }
  &__button {
    background-color: #c1c424;
    color: black;
    font-size: 16px;
    padding: 16px 30px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    text-align: center;
  }
}
  
</style>
