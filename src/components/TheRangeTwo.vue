<template>
  <div class="range">
    <div class="range__value">{{ value }}%</div>
    <div class="range__input">
      <input v-model="value" type="range" />
    </div>
    <div class="range__buttons">
      <button
        v-for="val in buttons"
        @click="value = val"
        :key="val"
        class="btn"
      >
        {{ val }}%
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TheRangeTwo",
  props: ["percentTwo"],
  data() {
    return {
      buttons: [25, 50, 75, 100],
     value:this.percentTwo
    };
  },
watch:{
  
}
};
</script>

<style scoped>
.range {
  width: 50%;
  margin: 50px auto;
  padding: 10px;
  background-color: rgb(33, 33, 104);
  font-family: sans-serif;
}
.range__value {
  color: rgba(255, 255, 255, 0.4);
}
input[type="range"] {
  margin: 10px auto;
  overflow: hidden;
  width: 100%;
  height: 30px;
  border-radius: 20px;
  -webkit-appearance: none;
  background: linear-gradient(to right, rgb(110, 247, 110), rgb(245, 86, 86));
}
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 26px;
  height: 26px;
  background-color: #fff;
  position: relative;
  border-radius: 20px;
}

.range__buttons {
  display: flex;
  justify-content: center;
}
.btn {
  display: inline-block;
  margin: 0 5px;
  line-height: 1.5;
  color: #fff;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  user-select: none;
  background-color: rgb(90, 107, 180);
  border: 1px solid transparent;
  padding: 5px 1rem;
  font-size: 1rem;
  border-radius: 1rem;
}
</style>