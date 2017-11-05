<template>
  <div>
    <div class="counter">
      <span>Counter: {{ count }}</span>
    </div>
  </div>
</template>

<script>
  export default {
    props: ['count'],

  }
</script>
