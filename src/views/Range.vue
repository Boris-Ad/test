<template>
   <the-range @newPercent="newPercent" :percent="percent"> </the-range>
    <the-range-two :percentTwo="percentTwo"> </the-range-two>
</template>

<script>
import TheRange from "../components/TheRange.vue";
import TheRangeTwo from "../components/TheRangeTwo.vue";
export default {
    name:'Range',
      data() {
    return {
      percent: 20,
      percentTwo: 20,
    };
  },

  methods: {
    newPercent(data) {
      this.percent = data;
    },
  },
components: { TheRange, TheRangeTwo },
}
</script>

<style>

</style>