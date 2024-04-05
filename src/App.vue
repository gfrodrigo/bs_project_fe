<template>
  <validate_credit/>
</template>

<script>
import validate_credit from "@/components/validate-credit.vue";

export default {
  name: 'App',
  components: {
    validate_credit
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  margin: 0;
  background: #eeee;
}
</style>
