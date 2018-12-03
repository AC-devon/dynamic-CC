<template>
  <div id="card-wrap">
    <div id="credit-card" :class="{ flipCard :typeCvv }">
      <!-- front of the credit card -->
      <div id="front-card">
        <div id="credit-conent">
          <div id="brand">
            <div id="provider-brand">BRAND</div>
            <div id="card-brand" >
               <transition name="fade">
              <font-awesome-icon v-if="icon" :icon="icon"/>
               </transition>
            </div>
          </div>
          <div id="card-number">
            <label id="card-label" :class="{ 'active-label': !numKey }">card number</label>
            <span id="cc">{{cc}}</span>
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
  computed: {
    icon () {

      let visaPattern = new RegExp("^4[0-9]{12}(?:[0-9]{3})?$");
      let mastPattern = new RegExp("^(?:5[1-5][0-9]{14})$");
      let amexPattern = new RegExp("^(?:3[47][0-9]{13})$");
      let discPattern = new RegExp("^(?:6(?:011|5[0-9][0-9])[0-9]{12})$");
      let dinersPattern = new RegExp("^3(?:0[0-5]|[68][0-9])[0-9]{11}$");
      let jcbPattern = new RegExp("^(?:2131|1800|35[0-9]{3})[0-9]{11}");
  
      let isVisa =
        visaPattern.test(this.cc.replace (/[A-Za-z|\s]/g, '')) === true;
      let isMast =
        mastPattern.test(this.cc.replace (/[A-Za-z|\s]/g, '')) === true;
      let isAmex =
        amexPattern.test(this.cc.replace (/[A-Za-z|\s]/g, '')) === true;
      let isDisc =
        discPattern.test(this.cc.replace (/[A-Za-z|\s]/g, '')) === true;
      let isDiners =
        dinersPattern.test(this.cc.replace (/[A-Za-z|\s]/g, '')) === true;
      let isJcb =
        jcbPattern.test(this.cc.replace (/[A-Za-z|\s]/g, '')) === true;
        let result;
      if (isVisa) {
        result =  "credit-card";
      } else if (isMast) {
         result =   "isMast";
      } else if (isAmex) {
         result =   "isAmex";
      } else if (isDisc) {
         result =   "isDisc";
      } else if (isDiners) {
         result =   "isDiners";
      } else if (isJcb) {
         result =   "isJcb";
      }
      return result;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
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
  transition: all 1s ease;
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
  font-size: 25px;
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
