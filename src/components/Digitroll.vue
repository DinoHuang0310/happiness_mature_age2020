<template>
  <div style="width:320px;">
    <DigitRoll :rollDigits="digits" />
  </div>
</template>

<script>
  import DigitRoll from '@huoyu/vue-digitroll';
  export default {
    components: { DigitRoll },
    data () {
      return {
        digits: 123456,
      }
    }
  }
</script>