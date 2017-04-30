<template>
  <header>

    <div class="session">
      <div class="breakCtrl">
        <p>break length</p>
        <button class="minus" @click="breakLengthChange(-1)">-</button><span class="time">{{breakLength}}</span>
        <button class="plus" @click="breakLengthChange(1)">+</button>
      </div>
      <div class="sessionCtrl">
        <p>session length</p>
        <button class="minus" @click="sessionLengthChange(-1)">-</button><span class="time">{{sessionLength}}</span>
        <button class="plus" @click="sessionLengthChange(1)">+</button>
      </div>
      <button class="btn-reset" @click="resetTimer">Reset</button>
    </div>
  </header>
</template>

<script>
  export default {
    props: ['breakLength', 'sessionLength'],
    methods: {
      breakLengthChange(val) {
        if (this.breakLength <= 0 && val === -1) {
          return
        } else {
          this.$emit("changeBreakLength", val)
        }

      },
      sessionLengthChange(val) {
        if (this.sessionLength <= 0 && val === -1) {
          return
        } else {
          this.$emit("changeSessionLength", val)
        }
      },
      resetTimer() {
        window.location.reload()
      }
    }
  }
</script>

<style>
  .btn-reset {
    border: none;
    width: 80px;
    border-radius: 5px;
    color: #333333;
    background-color: #fff
  }
  .btn-reset:hover {
    cursor: pointer;
  }
</style>