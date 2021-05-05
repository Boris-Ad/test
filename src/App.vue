<template>
  <the-range
  @newPercent="newPercent"
   :percent="percent"></the-range>
   
</template>

<script>

import TheRange from "./components/TheRange.vue";
export default {
  name: "App",
  data() {
    return {
      percent: 0,
    };
  },

  methods: {
    newPercent(data){
      this.percent = data;
     }
  },
  components: { TheRange},
};
</script>

<style>
</style>