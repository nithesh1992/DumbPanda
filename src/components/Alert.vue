<template>
  <div class="hello">
    <h6 class="alert_mono"> {{msg}} </h6>
  </div>
</template>

<script>
export default {
  name: 'Alert',
  props: {
    msg: String,
    type: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
