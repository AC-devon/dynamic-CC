<template>
  <div id="app">
    <Card v-bind="{year,month,cc,numKey,typeCvv,cvv}"/>
    <div id="key-board-wrap">
          <numKeyBoard
      v-if="step < 4"
      v-show="!numKey"
      v-bind="{typeCvv}"
      v-on:keyPressed="updateKeyPress($event)"
    />
    <dateKeyBoard v-if="step < 4" v-show="numKey" v-on:datePressed="datePressed($event)"/>
    </div>
    <level v-if="step < 4" :step="step"/>
    <pay-btn v-show="step >= 4" :style="{ bottom: bottom }"/>
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import numKeyBoard from "./components/numKeyBoard.vue";
import dateKeyBoard from "./components/dateKeyBoard.vue";
import Level from "./components/Level.vue";
import payBtn from "./components/payBtn.vue";

export default {
  name: "app",
  components: {
    numKeyBoard,
    dateKeyBoard,
    Card,
    Level,
    "pay-btn": payBtn
  },
  data() {
    return {
      step: 1,
      year: "xx",
      month: "xx",
      cvv: "xxx",
      cc: "xxxx xxxx xxxx xxxx",
      numKey: false,
      typeCvv: false,
      bottom: "-500px"
    };
  },
  methods: {
    updateStep(val) {
      this.step = val;
    },
    // active when child key has press
    updateKeyPress(item) {
      if (this.step == 3) {
        this.cvv = this.cvv.split("");
        this.cvv[item.index] = item.val;
        this.cvv = this.cvv.join("");
        if (item.index == 2) {
          this.numKey = !this.numKey;
          this.typeCvv = false;
          this.step = 4;
          setTimeout(() => {
            this.bottom = "0px";
          }, 500);
        }
      } else {
        if (item.val == "x") {
          this.cc = this.cc.split("");
          this.cc[item.index+1] = item.val;
          this.cc = this.cc.join("");
        }else{
                  this.cc = this.cc.split("");
        this.cc[item.index] = item.val;
        this.cc = this.cc.join("");
        }
        if (item.index == 18) {
          this.numKey = !this.numKey;
          this.step = 2;
        }
      }
    },
    datePressed(val) {
      if (val.year) {
        this.year = val.year;
      } else if (val.month) {
        let addZero = val.month;
        if (addZero.toString().length <= 1) {
          addZero = "0" + addZero;
        }
        this.month = addZero;
      }
        
      if (this.year != "xx" && this.month != "xx") {
        this.step = 3;
        this.typeCvv = true;
        this.numKey = !this.numKey;
      }
    }
  }
};
</script>

<style lang="scss">
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background: #116081;
  color: white;
  margin-top: 60px;
}
#app {
  max-width: 95%;
  margin: 0 auto;
}
* {
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
}
</style>
