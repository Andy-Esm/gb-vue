<template>
  <div class="calc">
    <div class="calc-body">
      <input
        type="text"
        class="calc-input"
        placeholder="Введите первое число"
        v-model.number="operand1"
      />
      <input
        type="text"
        class="calc-input"
        placeholder="Введите второе число"
        v-model.number="operand2"
      />
      <div class="btn-wrapper">
        <button class="btn-operation btn" @click="add()">+</button>
        <button class="btn-operation btn" @click="subtract()">-</button>
        <button class="btn-operation btn" @click="multiply()">*</button>
        <button class="btn-operation btn" @click="divide()">/</button>
        <button class="btn-operation btn" @click="exponet()">**</button>
        <button class="btn-operation btn" @click="integerDivide()">%</button>
      </div>
      <div class="number-wrapper">
        <button
          class="btn btn-num"
          v-show="show"
          v-for="(num, idx) of numbers"
          :key="idx"
          @click="inputNum(num)"
        >
          {{ num }}
        </button>
        <button class="btn btn-accent" @click="removeLast" v-show="show">
          &#129040;
        </button>
      </div>
      <div class="checkbox-wrapper">
        <label for="show-numbers">show numbers</label>
        <input
          type="checkbox"
          class="checkbox-item"
          id="show-numbers"
          v-model="show"
        />
        <label for="operand1-show">Operand-1</label>
        <input
          type="radio"
          class="checkbox-item"
          id="operand1-show"
          value="operand1"
          v-model="picked"
        />
        <label for="operand2-show">Operand-2</label>
        <input
          type="radio"
          class="checkbox-item"
          id="operand2-show"
          value="operand2"
          v-model="picked"
        />
      </div>
    </div>
    <span class="result"> Результат: {{ result }}</span>
  </div>
</template>

<script>
export default {
  name: "CalcApp",
  props: {
    msg: String,
  },
  data() {
    return {
      show: false,
      picked: "",
      result: "",
      operand1: "",
      operand2: "",
      numbers: [1, 2, 3, 4, 5, 7, 8, 9, 0],
    };
  },
  methods: {
    clearInputs() {
      this.operand1 = "";
      this.operand2 = "";
    },
    add() {
      if (Number.isInteger(this.char)) {
        this.result = this.operand1 + this.operand2;
        this.clearInputs();
      } else {
        this.result = parseInt(this.operand1) + parseInt(this.operand2);
        this.clearInputs();
      }
    },
    subtract() {
      this.result = this.operand1 - this.operand2;
      this.clearInputs();
    },
    multiply() {
      this.result = this.operand1 * this.operand2;
      this.clearInputs();
    },
    divide() {
      if (this.operand2 === 0) {
        alert("На ноль делить нельзя");
      } else {
        this.result = this.operand1 / this.operand2;
      }
      this.clearInputs();
    },
    exponet() {
      this.result = this.operand1 ** this.operand2;
      this.clearInputs();
    },
    integerDivide() {
      this.result = Math.floor(this.operand1 / this.operand2);
      this.clearInputs();
    },
    removeLast() {},
    inputNum(char) {
      if (this.picked === "operand1") {
        this.operand1 += char;
      } else {
        this.operand2 += char;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.calc {
  margin: 0 auto;
  max-width: 300px;
}
.calc-body {
  margin-inline: auto;
  max-width: 300px;
  width: 100%;
  display: flex;
  flex-direction: column;
}
.calc-input {
  padding: 8px;
  text-align: center;
}
.result {
  display: block;
  font-size: 16px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: left;
  color: lightcoral;
}
.btn-wrapper {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
}
.btn {
  height: 50px;
  width: 50px;
  font-size: 16px;
  color: #fff;
  border: 0;
  cursor: pointer;
  font-weight: 700;
}
.btn-num {
  background-color: #42b983;
  margin: 0 0 14px 0;
  width: 30px;
  height: 30px;
}
.btn-operation {
  background-color: coral;
}
.btn-num:hover {
  background-color: green;
}
.btn-operation:hover {
  background-color: chocolate;
}

.btn-accent {
  width: 30px;
  height: 30px;
  text-transform: uppercase;
  background-color: indianred;
}
.btn-accent:hover {
  background-color: #ea4343;
}
.checkbox-wrapper {
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  gap: 8px;
  margin: 0 0 14px 0;
}
</style>
