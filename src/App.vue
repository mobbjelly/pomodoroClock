<template>
  <div id="app">
    <app-session
      :breakLength="breakLength"
      :sessionLength="sessionLength"
      @changeBreakLength="breakLength += $event"
      @changeSessionLength="sessionLength += $event"></app-session>
    <app-timer
      :initTimeLeft="sessionLength"
      :breakLength="breakLength"></app-timer>
  </div>
</template>

<script>
  import Session from './Session.vue'
  import Timer from './Timer.vue'
  export default {
    data() {
      return {
        breakLength: 5,
        sessionLength: 25
      }
    },
    components: {
      appSession: Session,
      appTimer: Timer
    }
  }
</script>

<style>
</style>