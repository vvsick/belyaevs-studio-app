<template>
    <div class="card show" :id="'card-' + cardId">
      <span class="card__timer">{{timerDisplay}}</span>
      <div class="card__divider"></div>
      <div class="card__controls">
        <svg id="start" @click="toggleButton" width="17" height="20" viewBox="0 0 17 20" fill="#9E9E9E" xmlns="http://www.w3.org/2000/svg">
          <path v-if="!isRunning" d="M0 20V0L17 10L0 20Z" />
          <rect v-if="isRunning" x="7" width="3" height="20" />
          <rect v-if="isRunning" width="3" height="20" />
        </svg>
        <svg id="rewind" @click="rewindTimer" width="20" height="20" viewBox="0 0 20 20" fill="#9E9E9E" xmlns="http://www.w3.org/2000/svg">
          <rect width="20" height="20" />
        </svg>
      </div>
    </div>
</template>

<script>
  export default {
    name: 'Card',
    props: {
      cardId: {
        type: Number,
        required: true
      }
    },
    data: () => ({
        isRunning: false,
        timerId: null,
        hours: 0,
        minutes: 0,
        seconds: 0,
    }),
    methods: {
      toggleButton() {
        const card = document.querySelector(`#card-${this.cardId}`)
        console.log(card);
        this.isRunning = !this.isRunning
        if (this.isRunning) {
          this.startTimer()
          card.classList.add('active')
        } else {
          this.stopTimer()
        }
      },
      startTimer() {
        this.timerId = setInterval(() => {
          this.seconds++;
          if (this.seconds === 60) {
            this.minutes++
            this.seconds = 0
          }
          if (this.minutes === 60) {
            this.hours++
            this.minutes = 0
          }
        }, 1000);
      },
      stopTimer() {
        const card = document.querySelector(`#card-${this.cardId}`)
        clearInterval(this.timerId);
        card.classList.remove('active')
      },
      rewindTimer() {
        this.stopTimer()
        this.seconds = 0
        this.minutes = 0
        this.hours = 0
        this.isRunning = false
      }
    },
    computed: {
      timerDisplay() {
        let hours = this.hours < 10 ? '0' + this.hours : this.hours;
        let minutes = this.minutes < 10 ? '0' + this.minutes : this.minutes;
        let seconds = this.seconds < 10 ? '0' + this.seconds : this.seconds;
        if (this.hours === 0 && this.minutes === 0) {
          return seconds
        } else if (this.hours === 0 && this.minutes > 0) {
          return `${minutes}:${seconds}`
        } else {
          return `${hours}:${minutes}:${seconds}`;
        }
      }
    }
  }
</script>
  
<style scoped lang="scss">
  .card {
    width: 225px;
    height: 120px;
    background-color: #696969;
    position: relative;
    box-sizing: border-box;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    transition: all 0.4s ease-out;
  }

    .card__timer {
      height: 50%;
      display: flex;
      align-items: center;
    }
  
    .card__controls {
      height: 50%;
      width: 100%;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    .card__divider {
      position: absolute;
      width: 100%;
      height: 0.5px;
      top: 50%;
      background-color: #9E9E9E;
    }
    
    #start {
      margin-right: 48px;
    }

    .active {
      color: #FFFFFF;

      .card__divider {
        background-color: #FFFFFF;
      }

      svg {
        fill: #FFFFFF;
      }
    }
</style>  