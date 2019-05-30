<template>
  <div class="calculator">
    <span class="display">{{current || '0'}}</span>
    <span @click="clear" class="btn">C</span>
    <span @click="sign" class="btn">+/-</span>
    <span @click="percent" class="btn">%</span>
    <span @click="divide" class="btn operator">/</span>
    <span @click="append('7')" class="btn">7</span>
    <span @click="append('8')" class="btn">8</span>
    <span @click="append('9')" class="btn">9</span>
    <span @click="multiply" class="btn operator">*</span>
    <span @click="append('4')" class="btn">4</span>
    <span @click="append('5')" class="btn">5</span>
    <span @click="append('6')" class="btn">6</span>
    <span @click="minus" class="btn operator">-</span>
    <span @click="append('1')" class="btn">1</span>
    <span @click="append('2')" class="btn">2</span>
    <span @click="append('3')" class="btn">3</span>
    <span @click="plus" class="btn operator">+</span>
    <span @click="append('0')" class="btn zero">0</span>
    <span @click="dot" class="btn">.</span>
    <span @click="equal" class="btn operator">=</span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "",
      operator: null,
      previous: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      this.current =
        this.current.charAt(0) === "-"
          ? this.current.slice(1)
          : `-${this.current}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.current),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    }
  }
};
</script>
 
 <style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1/5;
  background-color: #333;
  color: white;
}
.zero {
  grid-column: 1/3;
}
.btn {
  background-color: #eee;
  border: 1px solid #999;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
 