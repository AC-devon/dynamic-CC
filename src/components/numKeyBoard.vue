<template>
  <div id="num-key-board">
    <div class="key" v-for="(item,index) in 9" :key="index" @click="keyPressed(item)">{{item}}</div>

    <div class="key" @click="keyPressed(0)">0</div>
    <div class="key" @click="keyPressed(46)">
      <i class="fas fa-backspace">go back</i>
    </div>
  </div>
</template>

<script>
export default {
  name: "numKeyBoard",
  props: {
    typeCvv: Boolean
  },
  data() {
    return {
      counter: -1,
      checkCvv: false
    };
  },
  methods: {
    keyPressed(item) {
      // notice parent what key has clicked
      this.counter++;
      let key = {
        val: item,
        index: this.counter
      };
      if (key.index == 3) {
        this.counter++;
      }
      if (key.index == 8) {
        this.counter++;
      }
      if (key.index == 13) {
        this.counter++;
      }

      //reset coutnter in case of finish typing cc
      if (key.index == 18) {
        this.counter = -1;
      }
      this.$emit("keyPressed", key);
    }
  }
};
</script>

<style lang="scss" scoped>
#num-key-board {
  max-width: 500px;
  margin: 0 auto;
  color: white;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-end;
}
.key {
  width: 33%;
  font-size: 18px;
  height: 50px;
  align-items: center;
  justify-content: center;
  display: flex;
  cursor: pointer;
}
</style>

