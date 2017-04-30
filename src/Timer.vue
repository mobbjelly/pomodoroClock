<template>
  <section @click="startTimer">
    <div class="timer">
      <p class="title">{{sessionName}}</p>
      <p>{{isStarted ? secondsToHms(timeLeft) : secondsToHms(initTimeLeft * 60)}}</p>
      <span class="fill" :style="{'height':fillHeight + '%', 'background':fillColor }"></span>
    </div>
  </section>
</template>

<script>
  export default {
    props: ['initTimeLeft', 'breakLength'],
    data() {
      return {
        timeLeft: 0,
        isStarted: false,
        sessionName: "Session",
        fillColor: '#99CC00',
        fillHeight: 0
      }
    },
    methods: {
      startTimer() {
        const vm = this
        if (!vm.isStarted) {
          vm.isStarted = true
          vm.timeLeft = vm.initTimeLeft * 60
          setInterval(function () {
            vm.timeLeft -= 1
          }, 1000)
        }
      },
      secondsToHms(d) {
        d = Number(d);
        const h = Math.floor(d / 3600);
        const m = Math.floor(d % 3600 / 60);
        const s = Math.floor(d % 3600 % 60);
        return (
          (h > 0 ? h + ":" + (m < 10 ? "0" : "") : "") + m + ":" + (s < 10 ? "0" : "") + s
        );
      }
    },
    watch: {
      timeLeft: function (timeVal) {
        if (timeVal <= 0) {
          const mp3File = 'sample.mp3'
          const audio = new Audio(mp3File)
          audio.play()
          if (this.sessionName === "Session") {
            this.timeLeft = this.breakLength * 60
            this.sessionName = 'Break!'
          } else {
            this.timeLeft = this.initTimeLeft * 60
            this.sessionName = 'Session'
          }
        } else {
          if (this.sessionName === "Session") {
            this.fillHeight = 100 - (timeVal / (this.initTimeLeft * 60)) * 100
          } else {
            this.fillHeight = 100 - (timeVal / (this.breakLength * 60)) * 100
          }
        }
      }
    }
  }
</script>