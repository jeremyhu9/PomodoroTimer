<template>
  <div class="timer">
    <p>{{ time.minutes }} : {{ time.seconds }}</p>
  </div>
</template>

<script>
  export default {
    props: ['time'],
    beforeMount () {
      if (this.time.seconds === 60) {
        this.time.seconds = '00'
      }
    },
    data () {
      return {
      }
    }
  }
</script>
