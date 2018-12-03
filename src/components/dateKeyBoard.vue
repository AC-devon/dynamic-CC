<template>
  <div id="date-key-board">
    <div id="month">
      <span>month</span>
      <div
        class="monthKey"
        v-for="(month,index) in 12"
        :key="index"
        @click="updateExp(month,'month')"
      >
        <span v-if="index < 9">0</span>
        {{month}}
      </div>
    </div>
    <div id="year">
      <span>year</span>
      <div class="yearKey" v-for="(i) in 8" :key="i" @click="updateExp(year+i,'year')">{{year+i}}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "dateKeyBoard",
  data() {
    return {
      year: new Date().getFullYear()
    };
  },
  methods: {
    updateExp(val, type) {
      // notice parent what key has clicked
      console.log(typeof val, type);
      let covertStr = val.toString();
      let value = {};
      if (type == "month") {
        value = {
          month: val
        };
      } else {
        value = {
          year: covertStr.substr(2, 3)
        };
      }
      this.$emit("datePressed", value);
    }
  }
};
</script>

<style scoped>
#date-key-board {
  display: flex;
  margin-top: 45px;
  justify-content: center;
  text-transform: uppercase;
}
#date-key-board span {
  text-align: left;
  display: block;
}
#month,
#year {
  flex: 50%;
}
.yearKey,
.monthKey {
  height: 40px;
  justify-content: center;
  align-items: center;
  display: inline-flex;
  cursor: pointer;
}
.monthKey {
  width: 30%;
}
.yearKey {
  width: 50%;
}
</style>
