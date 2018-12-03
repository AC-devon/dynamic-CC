<template>
  <div id="num-key-board">
    <div class="key" v-for="(item,index) in 9" :key="index" @click="keyPressed(item)">{{item}}</div>
    <div class="key" @click="keyPressed(0)">0</div>
    <div class="key" @click="keyPressed('del')">
      <font-awesome-icon icon="backspace"/>
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
      key: {
        val: "",
        index: -1
      },
      checkCvv: false
    };
  },
  methods: {
    keyPressed(item) {
      // notice parent what key has clicked
      if (item == "del" && this.key.index >= -1) {

        this.key.val = "x";
        this.key.index--;
        if (
          this.key.index == 3 ||
          this.key.index == 8 ||
          this.key.index == 13
        ) {
          this.key.index--;
        }
      } else if(item != "del") {
        this.key.val = item;
        this.key.index++;
      }

      if (
        (this.key.index == 4 && item != "del") ||
        (this.key.index == 9 && item != "del") ||
        (this.key.index == 14 && item != "del")
      ) {
        this.key.index++;
      }

      //reset coutnter in case of finish typing cc
      if (this.key.index == 19) {
        this.key.index = 0;
      }
      
      if (this.key.index >= -1) {
        this.$emit("keyPressed", this.key);
      }
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

