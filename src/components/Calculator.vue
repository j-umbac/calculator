<template>
  <h1>Vue Calculator</h1>
  <div class="calculator">
    <div class="display">{{ current || "0" }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="times" class="btn operator">x</div>
    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append(0)" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      previous: null,
      current: "",
      operator: null,
      operatorClicked: false,
      equalClicked: false,
    };
  },

  methods: {
    clear() {
      this.current = "";
      this.operator = null;
      this.operatorClicked = false;
      this.equalClicked = false;
    },
    sign() {
      if (this.current !== "" && this.current !== "0") {
        this.current =
          this.current.charAt(0) === "-"
            ? this.current.slice(1)
            : `-${this.current}`;
      }
    },
    percent() {
      if (this.current !== "")
        this.current = `${parseFloat(this.current) / 100}`;
    },
    append(number) {
      if (this.equalClicked == true) {
        this.current = "";
        this.equalClicked = false;
      }
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
        this.equalClicked = false;
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
      this.current = "";
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    times() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    minus() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    equal() {
      this.equalClicked = true;
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = 0;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: rgb(87, 87, 87);
  font-size: 50px;
}
.calculator {
  margin: 0 auto;
  width: 30rem;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-family: Helvetica;
}

.display {
  grid-column: 1/5;
  text-align: right;
  padding-right: 20px;
  background-color: gray;
  padding-top: 20px;
  padding-bottom: 20px;
  font-size: 60px;
  color: white;
}

.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #f2f2f2;
  border: 1px solid gray;
  padding-top: 10px;
  padding-bottom: 10px;
  color: rgb(37, 37, 37);
  user-select: none;
  cursor: pointer;
}

.btn:active {
  transform: scale(0.95);
}
.operator {
  background-color: orange;
  color: white;
}
</style>
