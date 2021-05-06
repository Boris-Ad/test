<template>
  <div class="range">
    <div class="range__value">{{ percent }}%</div>
    <div class="range__input">
      <div 
      @touchstart.prevent="scaleClick($event)" 
      @mousedown.prevent="scaleClick($event)" 
      ref="scale" class="scale">
        <div
          ref="chip"
          class="chip"
          :style="{ left: `calc(${percent}% - ${currentWidth}px)` }"
        ></div>
      </div>
    </div>
    <div class="range__buttons">
      <button
        v-for="val in buttons"
        @click="$emit('newPercent', val)"
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
  name: "TheRange",
  emits: ["newPercent"],
  props: ["percent"],
  data() {
    return {
      buttons: [25, 50, 75, 100],
      widthChip: 26,
      radiusChip: 13,
      myEvent: null,
      shift: null,
    };
  },
  methods: {
     checkE(e) {
      if (e.clientX) {
        this.myEvent = e;
      } else {
        this.myEvent = e.changedTouches[0];
      }
    },
     shiftChip(event) {
      this.checkE(event);
      this.shift =
        this.myEvent.clientX -
        this.$refs.scale.getBoundingClientRect().left -
        this.radiusChip;
    },

    scaleClick(event) {
     this.shiftChip(event)
       document.addEventListener("mousemove", this.mouseMove);
      document.addEventListener("mouseup", this.mouseUp);
      document.addEventListener("touchmove", this.mouseMove);
      document.addEventListener("touchend", this.mouseUp);
      this.$refs.chip.ondragstart = () => false;
    },

      mouseMove(event) {
    this.shiftChip(event)
    },
     mouseUp() {
      document.removeEventListener("mouseup", this.mouseUp);
      document.removeEventListener("mousemove", this.mouseMove);
      document.removeEventListener("touchmove", this.mouseMove);
      document.removeEventListener("touchend", this.mouseUp);
    },
  },
  computed: {
    scaleWidth() {
      return (
        parseInt(window.getComputedStyle(this.$refs.scale).width) -
        this.widthChip
      );
    },
    currentWidth() {
      if (this.percent != 0) {
        return (this.widthChip / 100) * this.percent;
      } else {
        return this.percent;
      }
    },
  },
  watch: {
    shift() {
      if (this.shift != 0) {
        let currentPercent = (this.shift / (this.scaleWidth / 100)).toFixed(1);
        if (currentPercent > 100) currentPercent = 100;
        if (currentPercent < 0) currentPercent = 0;
        this.$emit("newPercent", currentPercent);
      }
    },
  },
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

.scale {
  width: 100%;
  height: 30px;
  margin: 10px auto;
  border-radius: 20px;
  background: linear-gradient(to right, rgb(110, 247, 110), rgb(245, 86, 86));
}
.chip {
  width: 26px;
  height: 26px;
  background-color: #fff;
  position: relative;
  top: 2px;
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