<template>
  <div id="card-wrap">
    <div id="credit-card" :class="{ flipCard :typeCvv }">
      <!-- front of the credit card -->
      <div id="front-card">
        <div id="credit-conent">
          <div id="brand">
            <div id="provider-brand">leumi</div>
            <div id="card-brand">visa</div>
          </div>
          <div id="card-number">
            <label id="card-label" :class="{ 'active-label': !numKey }">card number</label>
            <input type="text" max-length="16" id="cc" v-model="cc">
          </div>
          <div id="card-exp">
            <label id="exp-label" :class="{ 'active-label': numKey }">exp date</label>
            <span id="month">{{month}}/</span>
            <span id="year">{{year}}</span>
          </div>
        </div>
      </div>
      <div id="back-card">
        <div id="cvv-contant">
          <div id="blackStrip"></div>
          <div id="cvv">
            <label id="cvv-label" :class="{ 'active-label': !numKey }">cvv</label>
            <div>{{cvv}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {};
  },
  props: {
    year: String,
    month: String,
    cvv: String,
    cc: String,
    numKey: Boolean,
    typeCvv: Boolean
  },
  methods: {}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#card-wrap {
  position: relative;
  width: 425px;
  height: 230px;
  max-width: 100%;
  margin: 0 auto;
}
#credit-card {
  position: absolute;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transition: all 0.5s ease;
  color: gray;
  text-transform: uppercase;
  text-align: left;
}
.flipCard {
  transform: rotateY(180deg);
}
#front-card {
  background: white;
  position: absolute;
  backface-visibility: hidden;
}
#back-card {
  background: white;
  position: absolute;
  backface-visibility: hidden;
  transform: rotateY(180deg);
}
#front-card,
#back-card {
  width: 100%;
  height: 100%;
  border-radius: 12px;
}
#credit-card .active-label {
  color: pink;
  transition: 0.3s ease;
}
#front-card label {
  display: block;
}
#credit-conent {
  margin: 0 40px;
  padding-top: 18px;
}
#brand {
  display: flex;
  justify-content: space-between;
}
#card-number {
  text-align: left;
  margin-top: 20px;
}
#card-label {
  transition: 0.3s ease;
}

#cc {
  border: 0;
  outline: 0;
  width: 100%;
  word-spacing: 8px;
  font-size: 26px;
  color: gray;
}

#card-exp {
  margin-top: 36px;
}
#cvv-contant {
  margin-top: 10%;
}
#blackStrip {
  background: black;
  width: 100%;
  height: 50px;
}
#cvv {
  text-align: right;
  width: 60%;
  margin: 6% auto;
}
</style>
